<template>
  <div class="main">
    <el-container>
      <!-- 左侧菜单栏 -->
      <el-aside width='200px'>
       <el-menu :default-openeds="defaultOpeneds" :default-active="defaultActive" :unique-opened="true" :router="true">
         <!-- 1 -->
         <el-menu-item index="/settings">
           <i class="el-icon-setting"></i>
           <span slot="title">全局设置</span>
         </el-menu-item>
        <!-- 2 -->
        <el-submenu index='table'>
          <template slot="title">
            <i class="el-icon-menu"></i>
            <span>桌台管理</span>
          </template>
          <el-menu-item-group>
            <el-menu-item index='/table/list'>桌台列表</el-menu-item>
            <el-menu-item index='/table/add'>添加桌台</el-menu-item>
            <el-menu-item index='/table/delete'>删除桌台</el-menu-item>
          </el-menu-item-group>
        </el-submenu>
        <!-- 3 -->
         <el-menu-item index="/category/list">
           <i class="el-icon-news"></i>
           <span slot="title">奶茶类别</span>
         </el-menu-item>
        <!-- 4 -->
        <el-submenu index='dish'>
          <template slot="title">
            <i class="el-icon-tickets"></i>
            <span>菜品管理</span>
          </template>
          <el-menu-item-group>
            <el-menu-item index='/dish/list'>菜品列表</el-menu-item>
            <el-menu-item index='/dish/add'>添加奶茶类</el-menu-item>
            <el-menu-item index='/dish/delete'>删除奶茶类</el-menu-item>
            <el-menu-item index='/dish/update'>修改奶茶类</el-menu-item>
          </el-menu-item-group>
        </el-submenu>

        <!-- 5 -->
         <el-menu-item index="/order/list">
           <i class="el-icon-date"></i>
           <span slot="title">订单管理</span>
         </el-menu-item>

         <el-menu-item index="/security">
           <i class="el-icon-bell"></i>
           <span slot="title">安全管理</span>
         </el-menu-item>

       </el-menu>
      </el-aside>
      <el-container>
        <!-- 顶部信息栏 -->
        <el-header height='60px'>
          <MainHeader></MainHeader>
        </el-header>
        <!-- 主体部分 -->
        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import MainHeader from '../components/MainHeader'
export default {
  data(){
    return{

    }
  },
  computed:{
    defaultActive(){
      return this.$route.path;
    },
    defaultOpeneds(){
      if(this.$route.path.indexOf('/table')==0){
        //用户当前在浏览的菜单项
        return ['table'];
      }else if(this.$route.path.indexOf('/dish')==0){
        return ['dish'];
      }else{
        return [];
      }
    }
  },
  beforeCreate(){
    //组件创建完
    if(!this.$store.state.adminName){
      this.$router.push('/login');//未登录就跳转登录页面
    }
  },
  components:{
     MainHeader
  }
}
</script>