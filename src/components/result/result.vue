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
          <el-input placeholder="请输入内容" v-model="input"></el-input>
          <el-button icon="el-icon-search" type="primary">点击扫描</el-button>
        </div>
        <!-- 搜索与添加区域结束 -->

        <!-- 搜索结果卡片展示区域开始 -->
        <div class="result-box">
          <div class="left">
            <el-card class="box-card" shadow="hover">
              <div slot="header" class="clearfix">
                <span>版本优选</span>
              </div>
              <el-table :data="tableData" @row-click="openDetails">
                <el-table-column label="序号" type="index" align="center"></el-table-column>
                <el-table-column prop="group_id" label="Group ID" show-overflow-tooltip></el-table-column>
                <el-table-column
                  prop="artifact_id"
                  label="Artifact ID"
                  show-overflow-tooltip
                  width="250px"
                ></el-table-column>
                <el-table-column prop="version" label="版本" align="center"></el-table-column>
              </el-table>
              <el-button type="small">查看更多</el-button>
            </el-card>
          </div>

          <div class="right">
            <el-card class="box-card" shadow="hover">
              <div slot="header" class="clearfix">
                <span>证书信息</span>
              </div>
              <el-table :data="tableData" @row-click="openDetails">
                <el-table-column label="序号" type="index" align="center"></el-table-column>
                <el-table-column prop="artifact_id" label="Artifact ID" show-overflow-tooltip></el-table-column>
                <el-table-column prop="license" label="证书" align="center"></el-table-column>
              </el-table>
              <el-button type="small">查看更多</el-button>
            </el-card>

            <el-card class="box-card" shadow="hover" style="margin-top:10px">
              <div slot="header" class="clearfix">
                <span>漏洞信息</span>
              </div>
              <div v-for="(item,index) in license_detail" :key="index">
                <span>{{item}}</span>
              </div>
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
        </div>-->
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
      tableData: [
        {
          artifact_id: 'spring-boot-starter-jdbc',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.0.6.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-thymeleaf',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.5.9.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-web',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.1.3.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'mybatis-spring-boot-starter',
          version: '2.0.1',
          group_id: 'org.mybatis.spring.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.3.2',
          stable_version: '2.1.1',
          license: 'Apache 2.0',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-jdbc',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.0.6.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-thymeleaf',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.5.9.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-web',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.1.3.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'mybatis-spring-boot-starter',
          version: '2.0.1',
          group_id: 'org.mybatis.spring.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.3.2',
          stable_version: '2.1.1',
          license: 'Apache 2.0',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-jdbc',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.0.6.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-thymeleaf',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.5.9.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-web',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.1.3.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'mybatis-spring-boot-starter',
          version: '2.0.1',
          group_id: 'org.mybatis.spring.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.3.2',
          stable_version: '2.1.1',
          license: 'Apache 2.0',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-jdbc',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.0.6.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-thymeleaf',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.5.9.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-web',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.1.3.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'mybatis-spring-boot-starter',
          version: '2.0.1',
          group_id: 'org.mybatis.spring.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.3.2',
          stable_version: '2.1.1',
          license: 'Apache 2.0',
          licenseList: null
        },
        {
          artifact_id: 'mysql-connector-java',
          version: '8.0.18',
          group_id: 'mysql',
          versionList: null,
          usageList: null,
          popular_version: '5.1.38',
          stable_version: '8.0.18',
          license: 'GPL 2.0',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-test',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.1.1.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-jdbc',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.0.6.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-thymeleaf',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.5.9.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-web',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.1.3.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'mybatis-spring-boot-starter',
          version: '2.0.1',
          group_id: 'org.mybatis.spring.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.3.2',
          stable_version: '2.1.1',
          license: 'Apache 2.0',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-jdbc',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.0.6.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-thymeleaf',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.5.9.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-web',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.1.3.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'mybatis-spring-boot-starter',
          version: '2.0.1',
          group_id: 'org.mybatis.spring.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.3.2',
          stable_version: '2.1.1',
          license: 'Apache 2.0',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-jdbc',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.0.6.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-thymeleaf',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.5.9.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-web',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.1.3.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'mybatis-spring-boot-starter',
          version: '2.0.1',
          group_id: 'org.mybatis.spring.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.3.2',
          stable_version: '2.1.1',
          license: 'Apache 2.0',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-jdbc',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.0.6.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-thymeleaf',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.5.9.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-web',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.1.3.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'mybatis-spring-boot-starter',
          version: '2.0.1',
          group_id: 'org.mybatis.spring.boot',
          versionList: null,
          usageList: null,
          popular_version: '1.3.2',
          stable_version: '2.1.1',
          license: 'Apache 2.0',
          licenseList: null
        },
        {
          artifact_id: 'mysql-connector-java',
          version: '8.0.18',
          group_id: 'mysql',
          versionList: null,
          usageList: null,
          popular_version: '5.1.38',
          stable_version: '8.0.18',
          license: 'GPL 2.0',
          licenseList: null
        },
        {
          artifact_id: 'spring-boot-starter-test',
          version: '2.2.0.RELEASE',
          group_id: 'org.springframework.boot',
          versionList: null,
          usageList: null,
          popular_version: '2.1.1.RELEASE',
          stable_version: '2.2.2.RELEASE',
          license: 'Apache 2.0  ',
          licenseList: null
        },
        {
          artifact_id: 'nekohtml',
          version: '1.9.21',
          group_id: 'net.sourceforge.nekohtml',
          versionList: null,
          usageList: null,
          popular_version: '1.9.12',
          stable_version: '1.9.22',
          license: 'Apache 2.0  ',
          licenseList: null
        }
      ],
      license_detail: [
        '强制要求衍生品开源:GPL 2.0  ',
        '不授权商标使用:Apache 2.0 ',
        '必须声明修改记录:Apache 2.0 GPL 2.0 ',
        '强制要求衍生品使用同一协议:GPL 2.0 '
      ],
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
  padding-top: 70px;
  background: rgb(250, 248, 248);
}
.el-aside {
  width: 250px !important;
  padding: 5px 0px 0px 5px;
  .box-card {
    height: 85vh;
    overflow: scroll;
  }
  .el-table {
    margin-top: 20px;
    height: 100%;
  }
}
.el-main {
  min-height: 90vh;
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
    .left {
      flex: 3;
    }
    .right {
      flex: 2;
    }
    .box-card {
      display: block;
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
        max-height: 60vh;
      }
    }
    .right .el-table {
      max-height: 29vh;
    }
  }

  .detail-box {
    margin-top: 20px;
  }
}
</style>
