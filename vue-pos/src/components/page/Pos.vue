<template>
  <div class="Pos">
    <el-row>
      <el-col :span="7"
              class="pos-order">
        <el-tabs>
          <el-tab-pane label="点餐">
            <el-table :data="tableData"
                      border
                      style="width:100%">
              <el-table-column prop="goodsName"
                               label="商品名称"
                               width="80%"></el-table-column>
              <el-table-column prop="count"
                               label="数量"
                               width="60"></el-table-column>
              <el-table-column prop="price"
                               label="价格"
                               width="70"></el-table-column>
              <el-table-column label="操作"
                               width="100"
                               fixed="right">
                <template slot-scope="scope">
                  <el-button type="text"
                             size="small"
                             @click="addOrder(scope.row)">增加</el-button>
                  <el-button type="text"
                             size="small"
                             @click="delOrder(scope.row)">删除</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div>
              <small>数量:{{this.totalnum}}</small>
              <small>总价:{{this.totalmoney}}</small>
            </div>
            <div class="div-btn">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger"
                         @click="delAll">删除</el-button>
              <el-button type="success">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单"></el-tab-pane>
          <el-tab-pane label="外卖"></el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col :span="15"
              class="pos-prodaction">
        <div class="often-food">
          <div class="title">常用商品</div>
          <div class="often-food-list">
            <ul>
              <li v-for="goods in oftenFood"
                  :key="goods.goodsName"
                  @click="addOrder(goods)">
                <span>{{goods.goodsName}}</span>
                <span style="color:blue;">{{goods.price}}</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="all-food">
          <el-tabs>
            <el-tab-pane label="汉堡">
              <ul>
                <li v-for="goods in allFood[0]"
                    :key="goods.goodsId"
                    @click="addOrder(goods)">
                  <span><img :src="goods.goodsImg"
                         alt="food"></span>
                  <span>{{goods.goodsName}}</span>
                  <span>{{goods.price}}</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="小食">
              <ul>
                <li v-for="goods in allFood[1]"
                    :key="goods.goodsId"
                    @click="addOrder(goods)">
                  <span><img :src="goods.goodsImg"
                         alt="food"></span>
                  <span>{{goods.goodsName}}</span>
                  <span>{{goods.price}}</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="饮料">
              <ul>
                <li v-for="goods in allFood[2]"
                    :key="goods.goodsId"
                    @click="addOrder(goods)">
                  <span><img :src="goods.goodsImg"
                         alt="food"></span>
                  <span>{{goods.goodsName}}</span>
                  <span>{{goods.price}}</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="套餐">
              <ul>
                <li v-for="goods in allFood[3]"
                    :key="goods.goodsId"
                    @click="addOrder(goods)">
                  <span><img :src="goods.goodsImg"
                         alt="food"></span>
                  <span>{{goods.goodsName}}</span>
                  <span>{{goods.price}}</span>
                </li>
              </ul>
            </el-tab-pane>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.pos-order {
  background-color: #f9f9f9;
  border-right: 1px solid grey;
}
.all-food {
  clear: both;
}
.div-btn {
  margin-top: 1rem;
}
li {
  display: flex;
  list-style: none;
  background-color: grey;
  float: left;
  padding: 0.3rem;
  margin: 0.3rem;
  align-items: center;
}
.title {
  text-align: left;
  padding: 0.1rem;
  height: 2rem;
  border-bottom: 1px solid grey;
}
img {
  max-width: 5rem;
}
</style>

<script>
import axios from 'axios'

export default {
  name: 'Pos',
  data () {
    return {
      tableData: [],
      oftenFood: [],
      allFood: [],
      totalnum: 0,
      totalmoney: 0
    }
  },
  created () { // 向后台请求商品数据
    axios.get('https://www.fastmock.site/mock/0bf6a5bae7eab8507e44b56191ddff36/vuepos/oftenGoods')
      .then(Response => {
        this.oftenFood = Response.data.oftenGoods
      })
      .catch(Error => {
        alert('网络请求失败，请刷新重试！')
      })
    axios.get('https://www.fastmock.site/mock/0bf6a5bae7eab8507e44b56191ddff36/vuepos/typeGoods')
      .then(response => {
        this.allFood = response.data.data
      })
      .catch()
  },
  mounted: function () { // 更改el-col的高度，使其撑满整个页面
    let orderHeight = document.body.clientHeight
    document.querySelector('.pos-order').style.height = orderHeight + 'px'
  },
  methods: {
    addOrder (goods) {
      // 判断点单中是否有对应商品
      let isHave = false
      for (let i = 0; i < this.tableData.length; i++) {
        if (this.tableData[i].goodsId === goods.goodsId) {
          isHave = true
        }
      }
      // 向点单中添加商品
      if (isHave) {
        let arr = this.tableData.filter(item => item.goodsName === goods.goodsName)
        arr[0].count++
      } else {
        let arr = {
          'goodsId': goods.goodsId,
          'goodsName': goods.goodsName,
          'price': goods.price,
          'count': 1
        }
        this.tableData.push(arr)
      }
      // 计算总数和总价
      this.totalnum = 0
      this.totalmoney = 0
      this.tableData.map(item => {
        this.totalnum += item.count
        this.totalmoney += item.count * item.price
      })
    },
    // 删除点单中对应商品
    delOrder (goods) {
      this.tableData.map((item, index) => {
        if (item.goodsId === goods.goodsId) {
          if (--this.tableData[index].count === 0) {
            this.tableData.splice(index, 1)
          }
        }
      })
      this.totalmoney -= goods.price
      this.totalnum--
    },
    delAll () {
      this.tableData = []
      this.totalnum = 0
      this.totalmoney = 0
    }
  }

}
</script>
