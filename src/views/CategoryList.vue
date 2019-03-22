<template>
  <div class="ydd-category-list">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">首页
      </el-breadcrumb-item>
      <el-breadcrumb-item >奶茶种类管理
      </el-breadcrumb-item>
      <el-breadcrumb-item >种类列表
      </el-breadcrumb-item>
    </el-breadcrumb>
    <br>
    <el-button type="primary" @click="addCategory">添加奶茶种类</el-button>
    <br>
    <el-table :data='categoryList' stripe border>
      <el-table-column label='编号' prop='cid'></el-table-column>
      <el-table-column label='名称' prop='cname'></el-table-column>

      <el-table-column label='操作'>
        <template slot-scope="{row,$index}">
          <el-button type="success" @click="updateCategory(row,$index)">修改</el-button>
          <el-button type="error" @click="deleteCategory(row,$index)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data(){
    return{
      categoryList:[]
    }
  },
  mounted(){
    var url=this.$store.state.globalSettings.apiUrl+'/admin/category';
    this.$axios.get(url).then((res)=>{
      this.categoryList=res.data;
    }).catch((err)=>{
      console.log(err);
    })
  },
  methods:{
    deleteCategory(c,i){
      this.$confirm('删除不可更改,确定删除吗?','提示',{type:'warning'}).then(()=>{
        var url=this.$store.state.globalSettings.apiUrl+'/admin/category/'+c.cid;
        this.$axios.delete(url).then((res)=>{
          if(res.data.code==200){
            this.categoryList.splice(i,1);
            this.$message.success('奶茶品种删除成功:')
            }else{
              this.$message.error('品种删除有误:'+res.data.msg)
            }
        }).catch((err)=>{
          console.log(err)
          })
      }).catch(()=>{

      })
      
    },
    updateCategory(c,i){
      this.$prompt('请输入您想修改的类别名:','提示',{
        inputValue:c.cname
      }).then(({value})=>{

      }).catch(()=>{

      })
    },
    addCategory(){
      this.$prompt('请输入新的奶茶种类:','提示',{type:'info'}).then(({value})=>{
        var url=this.$store.state.globalSettings.apiUrl+'/admin/category';
        this.$axios.post(url,{cname:value}).then((res)=>{
          if(res.data.code==200){
            this.$message.success('添加成功')
            this.categoryList.push({cid:res.data.cid,cname:value})
          }else{
            this.$message.error('添加失败:'+res.data.msg)
          }
        }).catch((err)=>{
          cosnole.log(err)
        })
      }).catch((err)=>{
         
      })
    }
  }
}
</script>