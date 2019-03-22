<template>
 <div class="ydd-main-header">
  <h3 class="ydd-title">{{$store.state.globalSettings.appName}}管理后台</h3>
  <div class="ydd-right">
   当前用户:{{$store.state.adminName}}
   <el-button @click="quit">退出</el-button>
  </div>
 </div>
</template>

<script>
export default {
 methods:{
  quit(){
   this.$store.commit('setAdminName','');
   this.$router.push('/login')

  }
 }
}
</script>


<style lang='scss'>
   $header-height:60px;

  .ydd-main-header{
   background:#dcdef6;
   border-radius: 4px;
   line-height: $header-height;
   height: $header-height;
   padding:0 6px;

   .ydd-title{
    color:#303133;
    float: left;
    margin: 0;
   }

   .ydd-right{
    float:right;
   }
  }
</style>
