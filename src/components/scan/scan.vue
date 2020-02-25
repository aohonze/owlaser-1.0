<template>
  <el-container class="scanPage">
    <!-- 上传部分盒子开始 -->
    <div class="upload-box">
      <el-upload
        class="upload-demo"
        ref="upload"
        action="http://114.116.114.218:8081/upload"
        :on-success="handleAvatarSuccess"
        :file-list="fileList"
        :auto-upload="false"
      >
        <el-button slot="trigger" class="selectFile-btn"
          >选取pom.xml文件</el-button
        >
        <el-button @click="submitUpload" class="uploadFile-btn"
          >开始扫描</el-button
        >
      </el-upload>
    </div>
    <!-- 上传部分盒子结束 -->
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      file: '',
      fileList: []
    }
  },

  methods: {
    submitUpload() {
      // console.log(this.$refs.upload.fileList)
      this.$refs.upload.submit()
      this.$message({
        message: '已上传成功，正在为您扫描，请稍等！',
        type: 'success'
      })
    },

    handleAvatarSuccess(response, file, fileList) {
      // 把上传后的返回值存入list
      this.$store.state.list = response.data
      this.$router.push('/result')
    }
  }
}
</script>

<style lang="less" scoped>
.scanPage {
  height: 800px;
  // background-image: url('../../assets/mty.png');
  .upload-box {
    position: absolute;
    margin: auto;
    width: 410px;
    height: 200px;
    left: 50%;
    top: 60%;
    transform: translateX(-50%) translateY(-50%);

    .selectFile-btn {
      width: 300px;
      height: 50px;
      font-size: 16px;
      border: 2px solid #2980b9;
    }

    .uploadFile-btn {
      margin-left: 5px;
      width: 100px;
      height: 50px;
      color: white;
      font-size: 16px;
      background: #2980b9;
      border: 0;
    }
    .uploadFile-btn:hover {
      background: white;
      color: #2980b9;
      border: 2px solid #2980b9;
    }
  }
}
</style>
