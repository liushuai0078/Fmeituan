<template>
  <div class="nav">
      <router-link class="nav-item" to="/goods">点餐
        <i class="line"></i>
      </router-link>
      <router-link class="nav-item" to="/ratings">评价{{commentNum}}
        <i class="line"></i>
      </router-link>
      <router-link class="nav-item" to="/seller">商家
        <i class="line"></i>
      </router-link>
  </div>
</template>

<script>
export default {
 props:{
   commentNum:{
     type:Number,
     default:0
   }
 }
 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.nav {
    display: flex;
    width: 100%;
    height: 40px;
    line-height: 40px;
    border-bottom: 1px solid #e4e4e4;
}
.nav-item{
    position: relative;
    flex: 1;
    text-align: center;
    font-size: 13px;
    text-decoration: none;
    color: #666;
}
/* 选中的样式 */
.nav .active{
    color: #ffbb22;
}
.nav .active .line{
    position: absolute;
    left: 50%;
    bottom: 0;
    margin-left: -10px;
    width: 20px;
    height:2px;
    display: inline-block;
    background: #ffbb22;


}
</style>
