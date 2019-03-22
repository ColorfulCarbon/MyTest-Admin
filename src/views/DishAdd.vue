<template>
  <div class="">
    <h1>添加菜品</h1>

    <el-form label-width="100px">
      <el-form-item label="菜品图片:">
      
        <el-upload class="ydd-uploader" :action="uploadAction" :on-success="doUploadSucc" name="dishImg" :show-file-list="true">
          <img v-if="imageUrl" :src="imageUrl">
        </el-upload>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data(){
    return {
      imageUrl:'',//要显示的预览图地址
      uploadAction:this.$store.state.globalSettings.apiUrl+'/admin/dish/image',
      formData:{
        title:'',
        imgUrl:"",
        price:'',
        detail:'',
        categoryId:''
      }
    }
  },
  methods:{
    doUploadSucc(res,file){
      console.log(res)
      this.formData.imgUrl=res.fileName
      this.imageUrl=URL.createObjectURL(file.raw);
    }
  }
}
</script>
<style lang="scss">
  .ydd-uploader{
    .el-upload{
      border:1px dotted #aaa;
      border-radius: 3px;
      cursor: pointer;
      width: 250px;
      height: 177px;
      overflow:hidden;
      &:hover{
        border-color: #409eff
      }
    }
    img{
      max-width: 100%;
    }
  }
</style>