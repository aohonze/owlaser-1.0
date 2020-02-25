<template>
  <el-container class="home-container">
    <!-- 顶栏导航栏开始 -->

    <el-header>
      <div class="logo">
        <span>OWLASER</span>
      </div>
      <el-menu
        :default-active="activeIndex"
        mode="horizontal"
        active-text-color="#2980b9"
      >
        <el-menu-item index="/">首 页</el-menu-item>
        <el-menu-item index="/proInfo">项目介绍</el-menu-item>
        <el-menu-item index="/teamStory">团队故事</el-menu-item>
        <el-menu-item index="/contanct">联系我们</el-menu-item>
        <el-button>登 录</el-button>
        <el-button>注 册</el-button>
      </el-menu>
    </el-header>
    <!-- 顶栏导航栏结束 -->

    <!-- 主体部分开始 -->
    <el-main>
      <div class="banner">
        <div class="center">
          <h1>OWLASER</h1>
          <p>OWLASER make your project more ....</p>
          <p>PKU-HUAWEI</p>
          <router-link to="/index">
            <el-button type="primary" class="start-btn">GET START</el-button>
          </router-link>
        </div>
      </div>
      <div class="pro-info" id="#proInfo">info</div>
      <div class="team-ifo" id="3">team</div>
    </el-main>
    <!-- 主体部分结束 -->

    <!-- 页脚部分开始 -->
    <my-footer></my-footer>
    <!-- 页脚部分结束 -->
  </el-container>
</template>

<script>
export default {
  methods: {
    // 页面向下滑动时固定导航栏
    fixHeader() {
      alert('dsa')
    },
    changePosition() {
      const str = this.$route.query
      console.log(str)
      if (str != null) {
        document.querySelector(str).scrollIntoView({ behavior: 'smooth' })
      }
    }
  },

  // 引入脚部组件
  components: [{ 'my-footer': () => import('./common/footer') }]
}
</script>

<style lang="less" scoped>
.home-container {
  height: 100%;
}
.el-header {
  display: flex;
  width: 100% !important;
  padding: 0 50px;
  justify-content: space-between;
  align-items: center;
  z-index: 999;
  height: 80px !important;
  background: black;

  * {
    color: white;
    background: black;
  }
  .logo {
    font-size: 30px;
  }
  .el-menu {
    display: flex;
    align-items: center;
    border: 0;
    height: 100%;
    .el-menu-item {
      font-size: 16px;
    }
    .el-menu-item:hover {
      color: #409eff !important;
      background: transparent !important;
    }
    .el-menu-item.is-active {
      color: #409eff !important;
      background: transparent !important;
    }
    .el-button {
      margin: 0 10px;
    }
    .el-button:hover {
      color: white;
      background: #2980b9;
    }
  }
}

.el-main {
  padding: 0;

  .banner {
    height: 800px;
    background-image: url('../assets/mty.png');
    background-size: cover;

    .start-btn {
      width: 200px;
      height: 50px;
      font-size: 20px;
      border: 2px solid #2980b9;
      background: transparent;
    }
    .start-btn:hover {
      transform: scale(1.1);
      border: 0;
      background: #2980b9;
    }
    .center {
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translateX(-50%) translateY(-50%);
      text-align: center;
      h1 {
        -webkit-text-stroke: 2px #2980b9;
        -webkit-text-fill-color: transparent;
        font-size: 150px;
        font-family: 'montserrat', sans-serif;
        margin-bottom: 20px;
      }
      p {
        font-size: 20px;
        color: #fff;
        margin-bottom: 20px;
      }
    }
  }
  .pro-info {
    height: 500px;
  }
  .team-ifo {
    height: 700px;
  }
}
</style>
