<template>
  <div class="left-nav">
    <ul>
      <li>
        <i class="icon iconfont icon-aliadd-cart"></i>
        <div>店铺</div>
      </li>
      <li>
        <i class="icon iconfont icon-alicaidanguanli"></i>
        <div>菜单管理</div>
      </li>
      <li>
        <i class="icon iconfont icon-alirmb"></i>
        <div>收银</div>
      </li>
      <li>
        <i class="icon iconfont icon-aligerenxinxi"></i>
        <div>个人信息</div>
      </li>
    </ul>
  </div>
</template>

<style>
.left-nav {
  color: white;
  font-size: 10px;
  height: 100%;
  background-color: teal;
  float: left;
  width: 5%;
}
.iconfont {
  font-size: 24px;
}
.left-nav ul {
  padding: 0px;
  margin: 0px;
}
.left-nav li {
  list-style: none;
  text-align: center;
  border-bottom: 1px solid turquoise;
  padding: 10px;
}
</style>

<script>
export default {
  name: 'LeftNav'
}
</script>
