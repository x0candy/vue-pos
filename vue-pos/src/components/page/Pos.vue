<template>
  <div class="Pos">
    <el-row>
      <el-col :span="7"
              class="pos-order">
        <el-tabs>
          <el-tab-pane label="点餐"></el-tab-pane>
          <el-tab-pane label="挂单"></el-tab-pane>
          <el-tab-pane label="外卖"></el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col :span="15"
              class="pos-prodaction">产品栏</el-col>
    </el-row>
  </div>
</template>

<style scoped>
.pos-order {
  background-color: #f9f9f9;
  border-right: 1px solid grey;
}
.pos-prodaction {
}
</style>

<script>
export default {
  name: 'Pos',
  mounted: function () { // 更改el-col的高度，使其撑满整个页面
    let orderHeight = document.body.clientHeight
    document.querySelector('.pos-order').style.height = orderHeight + 'px'
  }
}
</script>
