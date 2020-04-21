<template>
  <el-container>
    <!-- 左边区域开始 -->
    <el-aside>
      <!-- 搜索与列表区域 -->
      <el-card class="box-card">
        <div slot="header">
          <el-input placeholder="请输入组件名..." v-model="input">
            <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
        </div>

        <el-table :data="searchlist || dependenciesList" @row-click="openDetails">
          <el-table-column label="序号" type="index" width="40px" align="center"></el-table-column>
          <el-table-column prop="artifact_id" label="Artifact ID" show-overflow-tooltip></el-table-column>
        </el-table>
      </el-card>
    </el-aside>
    <!-- 左边区域结束 -->

    <!-- 右边主体开始 -->
    <el-main>
      <!-- 搜索与添加区域开始 -->
      <div class="search">
        <el-upload
          class="upload-demo"
          ref="upload"
          action="http://182.254.200.15:8081/upload"
          :on-success="handleAvatarSuccess"
          :auto-upload="false"
        >
          <el-button slot="trigger" class="selectFile-btn">选取pom.xml文件</el-button>
          <el-button icon="el-icon-search" @click="submitUpload" type="primary">开始扫描</el-button>
        </el-upload>
      </div>
      <!-- 搜索与添加区域结束 -->

      <!-- 搜索结果卡片展示区域开始 -->
      <div class="result-box">
        <el-card class="result-card" shadow="hover">
          <div slot="header" class="clearfix">
            <span>项目扫描结果</span>
          </div>
          <el-alert type=" error">你的项目一共有{{securList}}个组件包含漏洞！</el-alert>
          <div v-for="(item,index) in checkMessage.license_detail" :key="index">
            <el-alert type="error">{{ item }}</el-alert>
          </div>
        </el-card>
        <el-card class="license-card" shadow="hover">
          <div slot="header" class="clearfix">
            <span>版本优选</span>
          </div>
          <el-table :data="dependenciesList" @row-click="openDetails">
            <el-table-column label="序号" type="index" align="center"></el-table-column>
            <el-table-column prop="group_id" label="Group ID" show-overflow-tooltip></el-table-column>
            <el-table-column
              prop="artifact_id"
              label="Artifact ID"
              show-overflow-tooltip
              width="250px"
            ></el-table-column>
            <el-table-column prop="version" label="目前版本" align="center"></el-table-column>
            <el-table-column prop="popular_version" label="最热版本" align="center"></el-table-column>
            <el-table-column prop="stable_version" label="稳定版本" align="center"></el-table-column>
          </el-table>
          <el-button type="small">查看更多</el-button>
        </el-card>

        <el-card class="secur-card" shadow="hover" style="margin-top:10px">
          <div slot="header" class="clearfix">
            <span>漏洞信息</span>
          </div>
          <el-table :data="dependenciesList" @row-click="openDetails">
            <el-table-column label="序号" type="index" align="center"></el-table-column>
            <el-table-column prop="artifact_id" label="Artifact ID" show-overflow-tooltip></el-table-column>
            <el-table-column prop="license" label="证书" align="center"></el-table-column>
          </el-table>
          <el-button type="small">查看更多</el-button>
        </el-card>
      </div>
      <!-- 搜索结果卡片展示区域结束 -->
    </el-main>
    <!-- 右边主体结束 -->
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      dependenciesList: [],
      checkMessage: {},
      input: '',
      searchlist: null,
      securList: {}
    }
  },
  mounted() {
    // 组件创建完后获取数据，
    // 此时 data 已经被 observed 了
    this.fetchData()
    this.scanSecur()
  },

  watch: {
    // 如果路由有变化，会再次执行该方法
    $route: 'fetchData',

    // 左边框输入信息时候响应跳转
    input: function(value) {
      this.searchlist = this.dependenciesList.filter(item => {
        const regx = new RegExp(value)
        return item.artifact_id.search(regx) !== -1
      })
    }
  },
  methods: {
    // 将存在store里面的数据导入本页面
    fetchData() {
      const data = JSON.parse(sessionStorage.getItem('responseData'))
      this.dependenciesList =
        this.$store.state.scanResult.dependenciesList || data.dependenciesList
      this.checkMessage =
        this.$store.state.scanResult.checkMessage || data.checkMessage
    },

    async scanSecur() {
      for (const item of this.dependenciesList) {
        const { data: res } = await this.$http.get(
          'http://182.254.200.15:8081/security',
          {
            params: {
              groupId: 'org.apache.hbase',
              artifactId: 'hbase'
              // groupId: item.group_id,
              // artifactId: item.artifact_id
            }
          }
        )
        if (res.data.list.length !== 0) {
          this.securList[item.artifact_id] = res.data.list
        }
        // console.log(item.group_id)
        // console.log(item.artifact_id)
      }
      // console.log(this.securList)
    },
    openDetails(row) {
      // 点击表格中的一行时跳转到细节页面  把当前表格行的值作为参数
      this.$router.push({
        path: './detail',
        query: { group_id: row.group_id, artifact_id: row.artifact_id }
      })
    },
    submitUpload() {
      this.$refs.upload.submit()
      this.$message({
        message: '已上传成功，正在为您扫描，请稍等！',
        type: 'success'
      })
    },

    // 上传文件扫描结果返回
    handleAvatarSuccess(response, file, fileList) {
      // 把上传后的返回值存入list
      if (response.errno === 0) {
        this.$store.state.scanResult = response.data
        this.$router.push('/result')
      } else {
        this.$message({
          message: '文件扫描失败！请重试！',
          type: 'error'
        })
      }
    }
  }
}
</script>

<style lang="less" scoped>
.el-container {
  height: 100vh;
  padding: 75px 0 20px 0;
  background: rgb(250, 248, 248);
  .el-aside {
    width: 250px !important;
    height: 88vh;
    .box-card {
      height: 99%;
      .el-table {
        height: 88vh;
        margin-top: -20px;
        overflow: scroll;
      }
    }
  }
  .el-main {
    .search {
      height: 10vh;
      display: flex;
      align-items: center;
      .upload-demo {
        display: flex;
        align-items: center;
        .selectFile-btn {
          width: 300px;
          margin-right: 20px;
          font-size: 14px;
        }
      }
    }

    .result-box {
      .el-card {
        margin: 10px 10px 10px 0px;
        .clearfix:before,
        .clearfix:after {
          display: table;
          content: '';
        }
        .clearfix:after {
          clear: both;
        }
        .el-button {
          margin-top: 10px;
        }
        .el-alert {
          margin: 5px 0;
        }
      }
      .result-card {
        height: 300px;
        .el-table {
          height: 15vh;
          overflow: scroll;
          margin-top: -10px;
        }
      }
      .license-card {
        height: 50vh;
        .el-table {
          height: 35vh;
          overflow: scroll;
          margin-top: -10px;
        }
      }
      .secur-card {
        height: 50vh;
        .el-table {
          height: 35vh;
          overflow: scroll;
          margin-top: -10px;
        }
      }
    }
  }
}
</style>
