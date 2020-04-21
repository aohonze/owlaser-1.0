<template>
  <el-container class="home-container">
    <!-- 顶栏导航栏开始 -->
    <el-header>
      <div class="logo">
        <span>OWLASER</span>
      </div>
      <el-menu mode="horizontal" active-text-color="#2980b9">
        <el-menu-item index="/" @click="scrollTo('#banner')">首 页</el-menu-item>
        <el-menu-item index="proInfo" @click="scrollTo('#proInfo')">项目介绍</el-menu-item>
        <el-menu-item index="teamInfo" @click="scrollTo('#teamInfo')">团队故事</el-menu-item>
        <el-menu-item index="contact" @click="scrollTo('#contact')">联系我们</el-menu-item>
        <div class="menu-btn">
          <el-button>登 录</el-button>
          <el-button>注 册</el-button>
        </div>
      </el-menu>
    </el-header>
    <!-- 顶栏导航栏结束 -->

    <!-- 主体部分开始 -->
    <el-main>
      <div class="banner" id="#banner">
        <img src="https://cdn.jsdelivr.net/gh/tyrone-wu/PicRepo/mty.png" />
        <div class="center">
          <h1>OWLASER</h1>
          <p>OWLASER make your project more ....</p>
          <p>PKU-HUAWEI</p>
          <router-link to="/index">
            <el-button type="primary" class="start-btn">GET START</el-button>
          </router-link>
        </div>
      </div>
      <div class="pro-info" id="#proInfo">
        <div class="pro-info-intro">
          <h3>OWLASER</h3>
          <p>帮助您全方位审视项目当中的潜在问题！</p>
        </div>
        <img src="https://cdn.jsdelivr.net/gh/tyrone-wu/PicRepo/owlaser.png" />
      </div>
      <div class="team-info" id="#teamInfo">
        <div class="pic-box">
          <el-carousel :interval="4000" type="card" height="400px">
            <el-carousel-item v-for="item in 4" :key="item">
              <h3 class="medium">{{ item }}</h3>
            </el-carousel-item>
          </el-carousel>
        </div>
        <div class="team-info-intro">
          TEAM
          <p>北大-华为实验班开源组件健康扫描项目全体成员！</p>
        </div>
      </div>
      <div class="contact" id="#contact"></div>
    </el-main>
    <!-- 主体部分结束 -->

    <!-- 页脚部分开始 -->
    <my-footer></my-footer>
    <!-- 页脚部分结束 -->
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      menuList: []
    }
  },
  methods: {
    // 点击导航栏标签  页面滑动到相应的锚点
    scrollTo(str) {
      var el = document.getElementById(str)
      this.$nextTick(function() {
        window.scrollTo({ behavior: 'smooth', top: el && el.offsetTop - 80 })
      })
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
  position: fixed;
  display: flex;
  width: 100% !important;
  padding: 0 50px;
  justify-content: space-between;
  align-items: center;
  z-index: 999;
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
      height: 100%;
      font-size: 16px;
    }
    .el-menu-item:hover {
      color: #409eff !important;
      background: transparent !important;
      border-bottom: 2px solid #409eff !important;
    }
    .el-menu-item.is-active {
      color: #409eff !important;
      background: transparent !important;
    }
    .menu-btn {
      width: 200px;
      .el-button {
        margin: 0 10px;
      }
      .el-button:hover {
        color: white;
        background: #2980b9;
        border: 1px solid #2980b9;
      }
    }
  }
}

.el-main {
  padding: 0;
  .banner {
    height: 100vh;
    overflow: hidden;
    img {
      width: 100%;
      animation: move 20s infinite;
    }
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
    height: 700px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    .pro-info-intro {
      font-size: 50px;

      p {
        font-size: 30px;
      }
    }
    img {
      height: 400px;
      transform: rotate(10deg);
    }
  }
  .team-info {
    height: 800px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    .team-info-intro {
      font-size: 50px;

      p {
        font-size: 30px;
      }
    }
    .pic-box {
      width: 800px;
      .el-carousel__item h3 {
        color: #475669;
        font-size: 14px;
        opacity: 0.75;
        line-height: 200px;
        margin: 0;
      }

      .el-carousel__item:nth-child(2n) {
        background-color: #99a9bf;
      }

      .el-carousel__item:nth-child(2n + 1) {
        background-color: #d3dce6;
      }
    }
  }
}

@keyframes move {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}
</style>
