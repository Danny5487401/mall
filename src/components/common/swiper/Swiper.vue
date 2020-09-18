<template>
  <div id="hy-swiper">
    <div class="swiper">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "Swiper",
  mounted: function () {
    // 1.操作DOM, 在前后添加Slide
    setTimeout(() => {
      this.handleDom();

      // 2.开启定时器
      this.startTimer();
    }, 100);
  },
  props: {
    interval: {
      type: Number,
      default: 3000,
    },
    animDuration: {
      type: Number,
      default: 300,
    },
  },
  data: function () {
    return {
      slideCount: 0, // 元素个数
      totalWidth: 0, // swiper的宽度
      // swiperStyle: {}, // swiper样式
      currentIndex: 1, // 当前的index
      scrolling: false, // 是否正在滚动
    };
  },
  methods: {
    handleDom: function () {
      // 1.获取要操作的元素
      let swiperEl = document.querySelector(".swiper");
      let slidesEls = swiperEl.getElementsByClassName("slide");

      // 2.保存个数
      this.slideCount = slidesEls.length;
      console.log(swiperEl);
      console.log(slidesEls);

      // // 3.如果大于1个, 那么在前后分别添加一个slide
      if (this.slideCount > 1) {
        let cloneFirst = slidesEls[0].cloneNode(true);
        let cloneLast = slidesEls[this.slideCount - 1].cloneNode(true);
        swiperEl.insertBefore(cloneLast, slidesEls[0]);
        swiperEl.appendChild(cloneFirst);
        this.totalWidth = swiperEl.offsetWidth;
        this.swiperStyle = swiperEl.style;
      }

      // 4.让swiper元素, 显示第一个(目前是显示前面添加的最后一个元素)
      this.setTransform(-this.totalWidth);
    },
    /**
     * 设置滚动的位置
     */
    setTransform: function (position) {
      this.swiperStyle.transform = `translate3d(${position}px, 0, 0)`;
      this.swiperStyle[
        "-webkit-transform"
      ] = `translate3d(${position}px), 0, 0`;
      this.swiperStyle["-ms-transform"] = `translate3d(${position}px), 0, 0`;
    },
    startTimer: function () {
      this.playTimer = window.setInterval(() => {
        this.currentIndex++;
        this.scrollContent(-this.currentIndex * this.totalWidth);
      }, this.interval);
    },
    /**
     * 滚动到正确的位置
     */
    scrollContent: function (currentPosition) {
      // 0.设置正在滚动
      this.scrolling = true;

      // 1.开始滚动动画
      this.swiperStyle.transition = "transform " + this.animDuration + "ms";
      this.setTransform(currentPosition);

      // 2.判断滚动到的位置
      this.checkPosition();

      // 4.滚动完成
      this.scrolling = false;
    },
    /**
     * 校验正确的位置
     */
    checkPosition: function () {
      window.setTimeout(() => {
        // 1.校验正确的位置
        this.swiperStyle.transition = "0ms";
        if (this.currentIndex >= this.slideCount + 1) {
          this.currentIndex = 1;
          this.setTransform(-this.currentIndex * this.totalWidth);
        } else if (this.currentIndex <= 0) {
          this.currentIndex = this.slideCount;
          this.setTransform(-this.currentIndex * this.totalWidth);
        }

        // 2.结束移动后的回调
        this.$emit("transitionEnd", this.currentIndex - 1);
      }, this.animDuration);
    },
  },
};
</script>

<style scoped>
#hy-swiper {
  overflow: hidden;
  position: relative;
}
.swiper {
  display: flex;
}
</style>