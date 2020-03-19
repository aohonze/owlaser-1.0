<template>
  <div>
    <el-container>
      <!-- 左边区域开始 -->
      <el-aside>
        <!-- 搜索与列表区域 -->
        <el-card class="box-card">
          <el-input placeholder="请输入组件名...">
            <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
          <el-table :data="tableData" @row-click="openDetails">
            <el-table-column
              prop="artifact_id"
              label="Artifact ID"
            ></el-table-column>
          </el-table>
        </el-card>
      </el-aside>
      <!-- 左边区域结束 -->

      <!-- 右边主体开始 -->
      <el-main>
        <!-- 搜索与添加区域开始 -->
        <div class="search">
          <el-input placeholder="请输入内容" v-model="input"> </el-input>
          <el-button icon="el-icon-search" type="primary">点击扫描</el-button>
        </div>
        <!-- 搜索与添加区域结束 -->

        <!-- 搜索结果卡片展示区域开始 -->
        <div class="result-box">
          <el-card class="box-card" shadow="hover">
            <div slot="header" class="clearfix">
              <span>版本优选</span>
            </div>
            <el-table :data="tableData" @row-click="openDetails">
              <el-table-column label="序号" type="index"></el-table-column>
              <el-table-column
                prop="artifact_id"
                label="Artifact ID"
              ></el-table-column>
              <el-table-column prop="version" label="版本"></el-table-column>
            </el-table>
            <el-button type="small">查看更多</el-button>
          </el-card>

          <div class="right">
            <el-card class="box-card" shadow="hover">
              <div slot="header" class="clearfix">
                <span>证书信息</span>
              </div>
              <el-table :data="tableData" @row-click="openDetails">
                <el-table-column label="序号" type="index"></el-table-column>
                <el-table-column
                  prop="artifact_id"
                  label="Artifact ID"
                ></el-table-column>
                <el-table-column prop="license" label="证书"></el-table-column>
              </el-table>
              <el-button type="small">查看更多</el-button>
            </el-card>

            <el-card class="box-card" shadow="hover" style="margin-top:10px">
              <div slot="header" class="clearfix">
                <span>漏洞信息</span>
              </div>
              <el-table :data="tableData" @row-click="openDetails">
                <el-table-column label="序号" type="index"></el-table-column>
                <el-table-column
                  prop="artifact_id"
                  label="Artifact ID"
                ></el-table-column>
              </el-table>
              <el-button type="small">查看更多</el-button>
            </el-card>
          </div>
        </div>
        <!-- 搜索结果卡片展示区域结束 -->

        <!-- 全部结果展示区域开始 -->
        <!-- <div class="detail-box">
          <el-card>
            <el-table :data="tableData" @row-click="openDetails">
              <el-table-column label="序号" type="index"></el-table-column>
              <el-table-column
                prop="group_id"
                label="Group ID"
              ></el-table-column>
              <el-table-column
                prop="artifact_id"
                label="Artifact ID"
              ></el-table-column>
              <el-table-column prop="version" label="版本"></el-table-column>

              <el-table-column
                prop="popular_version"
                label="推荐版本"
              ></el-table-column>
              <el-table-column
                prop="stable_version"
                label="稳定版本"
              ></el-table-column>
              <el-table-column prop="license" label="证书"></el-table-column>
            </el-table>
          </el-card>
        </div> -->
        <!-- 全部结果展示区域开始结束 -->
      </el-main>
      <!-- 右边主体结束 -->
    </el-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [],
      input: ''
    }
  },
  created() {
    // 组件创建完后获取数据，
    // 此时 data 已经被 observed 了
    this.fetchData()
  },
  watch: {
    // 如果路由有变化，会再次执行该方法
    $route: 'fetchData'
  },
  methods: {
    // 将存在store里面的数据导入本页面
    fetchData() {
      for (const item in this.$store.state.list.list) {
        this.tableData.push(this.$store.state.list.list[item])
      }
    },
    openDetails(row) {
      // 点击表格中的一行时跳转到细节页面  把当前表格行的值作为参数
      this.$router.push({
        path: './detail',
        query: { group_id: row.group_id, artifact_id: row.artifact_id }
      })
    }
  }
}
</script>

<style lang="less" scoped>
.el-container {
  background: rgb(250, 248, 248);
}
.el-aside {
  width: 250px !important;
  padding: 5px 0px 0px 5px;
  .el-table {
    margin-top: 20px;
    min-height: 450px;
  }
}
.el-main {
  .search {
    display: flex;
    .el-input {
      width: 250px;
    }
    .el-button {
      margin-left: 20px;
    }
  }

  .result-box {
    display: flex;
    margin-top: 20px;
    .box-card {
      display: block;
      width: 480px;
      margin-right: 10px;
      .text {
        font-size: 14px;
      }
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
      .el-table {
        margin-top: -10px;
        max-height: 300px;
      }
    }
    .right .el-table {
      max-height: 100px;
    }
  }

  .detail-box {
    margin-top: 20px;
  }
}
</style>
