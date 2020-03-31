<template>
  <div class="bar">
    <div class="box">
      <ul @touchstart="handleTouchStart" @touchmove="handleTouchMove" @touchend="handleTouchend">
        <li class="nav_box">
          <img src="./../../../static//img//1.png" alt />
          <span class="nav_title">热门</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//2.png" alt />
          <span class="nav_title">男装</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//3.png" alt />
          <span class="nav_title">女装</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//4.png" alt />
          <span class="nav_title">儿童玩具</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//5.png" alt />
          <span class="nav_title">书籍</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//1.png" alt />
          <span class="nav_title">优惠券</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//2.png" alt />
          <span class="nav_title">外卖</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//3.png" alt />
          <span class="nav_title">折口专区</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//4.png" alt />
          <span class="nav_title">特价区</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//5.png" alt />
          <span class="nav_title">电子产品</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//1.png" alt />
          <span class="nav_title">热门</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//2.png" alt />
          <span class="nav_title">男装</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//3.png" alt />
          <span class="nav_title">女装</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//4.png" alt />
          <span class="nav_title">儿童玩具</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//5.png" alt />
          <span class="nav_title">书籍</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//1.png" alt />
          <span class="nav_title">优惠券</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//2.png" alt />
          <span class="nav_title">外卖</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//3.png" alt />
          <span class="nav_title">折口专区</span>
        </li>
        <li class="nav_box">
          <img src="./../../../static//img//3.png" alt />
          <span class="nav_title">折口专区</span>
        </li>
      </ul>
      <div class="scroll">
        <div class="scrollColre" :style="innerBarStyle"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      screenW:
        window.innerWidth ||
        document.documentElement.clientWidth ||
        document.body.clientWidth, //屏幕的宽度
      scrollContent: 810, //内容的宽度
      bgBarW: 50, //滚动背景默认长度
      barXWidth: 0, //滚动条长度
      startX: 0, //触摸监听起点
      endFlag: 0, //结束点
      barMoveWidth: 0 //移动的距离
    };
  },
  created() {},
  computed: {
    innerBarStyle() {
      return {
        width: `${this.barXWidth}px`,
        left: `${this.barMoveWidth}px`
      };
    }
  },
  watch: {},
  methods: {
    // 1、获取滚动条的宽度
    getBottomBarWidth() {
      this.barXWidth = this.bgBarW * (this.screenW / this.scrollContent);
    },
    // 2、监听事件(无用)
    bindEvent() {
      this.$el.addEventListener("touchstart", this.handleTouchStart, false);
      this.$el.addEventListener("touchmove", this.handleTouchMove, false);
      this.$el.addEventListener("touchend", this.handleTouchend, false);
    },
    // 开始触摸
    handleTouchStart(event) {
      let touch = event.touches[0];
      //  求出起始点
      this.startX = Number(touch.pageX);
    },
    // 开始移动
    handleTouchMove(event) {
      //  获取第一个触点
      let touch = event.touches[0];
      // 求出移动的距离
      let moveWidth = Number(touch.pageX) - this.startX;
      // console.log(moveWidth)
      // 求出滚动条走的距离
      this.barMoveWidth = -(
        moveWidth * (this.bgBarW / this.scrollContent) -
        this.endFlag
      );
      if (this.barMoveWidth <= 0) {
        this.barMoveWidth = 0;
      } else if (this.barMoveWidth > this.bgBarW - this.barXWidth) {
        this.barMoveWidth = this.bgBarW - this.barXWidth;
      }
    },
    // 结束触摸
    handleTouchend(event) {
      this.endFlag = this.barMoveWidth;
    }
  },
  mounted() {
    // nav滚动条
    this.getBottomBarWidth();
  }
};
</script>
<style scoped>
.bar {
  width: 100%;
  height: 100%;
}
.box {
  width: 100%;
  height: 190px;
  /* background: darkcyan; */
  overflow-y: hidden;
}
.box::-webkit-scrollbar {
  display: none;
}
.box ul {
  width: 810px;
  height: 100%;
  display: flex;
  flex-wrap: wrap;
}
.box ul li {
  width: 90px;
  height: 90px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.box ul li:nth-child(odd) {
  /* background: darkkhaki; */
}
.box ul li:nth-child(even) {
  /* background: darkorchid; */
}
.box img {
  width: 60%;
  /* margin-bottom: 5px; */
}
.box .nav_title {
  font-size: 14px;
  color: #666666;
}
.box .scroll {
  width: 50px;
  height: 5px;
  border: 1px solid #ddd;
  background: #ddd;
  position: absolute;
  border-radius: 30px;
  left: 50%;
  margin-left: -25px;
  margin-top: -12px;
}
.box .scroll .scrollColre {
  height: 100%;
  position: absolute;
  background: crimson;
  border-radius: 30px;
}
</style>