<template>
  <el-container>
    <!-- 左边区域开始 -->
    <el-aside>
      <!-- 搜索与列表区域 -->
      <el-card class="box-card">
        <el-input placeholder="请输入组件名...">
          <el-button slot="append" icon="el-icon-search"></el-button>
        </el-input>
        <el-table :data="tableData" @row-click="openDetails">
          <el-table-column prop="artifact_id" label="Artifact ID"></el-table-column>
        </el-table>
      </el-card>
    </el-aside>
    <!-- 左边区域结束 -->
    <!-- 右边主体开始 -->
    <el-main>
      <el-table
        ref="filterTable"
        :data="tableData"
        style="width: 100%"
        @row-click="downLoadDependency"
      >
        <el-table-column label="序号" type="index"></el-table-column>
        <el-table-column prop="child_artifactid" label="child_artifactid"></el-table-column>
        <el-table-column prop="child_groupid" label="child_groupid" sortable></el-table-column>
        <el-table-column prop="url" label="url" width="500px"></el-table-column>
      </el-table>
    </el-main>
    <!-- 右边主体结束 -->
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      tableData: []
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
    async fetchData() {
      const dependencyInfo = this.$route.query
      const { data: res } = await this.$http.get(
        'http://114.116.114.218:8081/getdependency',
        {
          params: {
            groupId: dependencyInfo.group_id,
            artifactId: dependencyInfo.artifact_id
          }
        }
      )
      // 将得到的数据渲染到表格当中
      for (const item in res.data.list) {
        this.tableData = this.tableData.concat(res.data.list[item])
      }
    },
    // 用户点击具体的组件   跳转到MavenRepository
    downLoadDependency(row) {
      window.open(row.url)
    }
  }
}
</script>

<style lang="less" scoped>
.el-container {
  padding-top: 70px;
  .el-aside {
    width: 250px !important;
    min-height: 100vh;
    padding: 5px 0px 0px 5px;
    .el-table {
      margin-top: 20px;
      min-height: 70vh;
    }
  }
  .el-main {
    min-height: 100vh;
  }
}
</style>
