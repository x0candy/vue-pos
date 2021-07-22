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
                               width="100"></el-table-column>
              <el-table-column prop="count"
                               label="数量"
                               width="90"></el-table-column>
              <el-table-column prop="price"
                               label="价格"
                               width="90"></el-table-column>
              <el-table-column label="操作"
                               width="100"
                               fixed="right">
                <template>
                  <el-button type="text"
                             size="small">增加</el-button>
                  <el-button type="text"
                             size="small">删除</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="div-btn">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger">删除</el-button>
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
                  :key="goods.goodsName">
                <span>{{goods.goodsName}}</span>
                <span style="color:blue;">{{goods.price}}</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="all-food">
          <el-tabs>
            <el-tab-pane label="汉堡">汉堡</el-tab-pane>
            <el-tab-pane label="小食">小食</el-tab-pane>
            <el-tab-pane label="饮料">饮料</el-tab-pane>
            <el-tab-pane label="套餐">套餐</el-tab-pane>
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
  list-style: none;
  background-color: grey;
  float: left;
  padding: 0.3rem;
  margin: 0.3rem;
}
.title {
  text-align: left;
  padding: 0.1rem;
  height: 2rem;
  border-bottom: 1px solid grey;
}
</style>

<script>
export default {
  name: 'Pos',
  data () {
    return {
      tableData: [{
        goodsName: '可口可乐',
        price: 8,
        count: 1
      }, {
        goodsName: '香辣鸡腿堡',
        price: 15,
        count: 1
      }, {
        goodsName: '爱心薯条',
        price: 8,
        count: 1
      }, {
        goodsName: '甜筒',
        price: 8,
        count: 1
      }],
      oftenFood: [
        {
          goodsName: '香辣鸡腿堡',
          price: 15,
          count: 1
        }, {
          goodsName: '爱心薯条',
          price: 8,
          count: 1
        }, {
          goodsName: '甜筒',
          price: 8,
          count: 1
        }
      ]
    }
  },
  mounted: function () { // 更改el-col的高度，使其撑满整个页面
    let orderHeight = document.body.clientHeight
    document.querySelector('.pos-order').style.height = orderHeight + 'px'
  }
}
</script>
