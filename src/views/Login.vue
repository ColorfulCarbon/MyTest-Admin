<template>
  <div class="login">
    <el-card class="ydd-login-card">
      <div slot="header">管理员登录</div>
      <div>
        <el-form label-width="80px">

          <el-form-item label="管理员名:">
            <el-input v-model="formData.aname" placeholder="请输入管理员ID"></el-input>
          </el-form-item>

          <el-form-item label="登录密码:">
            <el-input v-model="formData.apwd" type="password" placeholder="请输入管理员密码"></el-input>
          </el-form-item>

          <el-form-item class="ydd-button">
            <el-button type="primary" @click=doLogin>登录</el-button>
            <el-button @click="doCancel">取消</el-button>
          </el-form-item>

        </el-form>
      </div>
    </el-card>
    {{$store.state.globalSettings}}
  </div>
</template>

<script>
export default {
  data(){
    return {
      formData:{ //表单框里的两个数据
        aname:'admin',
        apwd:'123456' 
      }
    }
  },
  methods:{
    doLogin(){
      var url=this.$store.state.globalSettings.apiUrl+`/admin/login/${this.formData.aname}/${this.formData.apwd}`;
      
      this.$axios.get(url).then((res)=>{
        if(res.data.code==200){
          this.$store.commit('setAdminName',this.formData.aname);
          this.$router.push('/main');
        }else{
          this.$alert('用户名或密码有误','登录失败',{type:'error'}).then(()=>{}).catch(()=>{})
        }

      }).catch((err)=>{
        console.log(err);
      })
    },
    doCancel(){
      this.formData.aname='';
      this.formData.apwd='';
    },
  },
}
</script>   


<style lang="scss">
  .ydd-login-card{
    width: 400px;
    margin: 150px auto;

    .el-card__header{
      text-align: center;
      font-size: 1.2em;
    }
  }

  .el-form{
    .ydd-button{
      text-align: center;
      margin:0px;
    }
    
  }
</style>