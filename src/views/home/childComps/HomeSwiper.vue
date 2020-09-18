<template>
  <Swiper>
    <template>
      <swiper-item v-for="item in banners" :key="item">
        <template>
          <a>
            <img :src="item" alt />
          </a>
        </template>
      </swiper-item>
    </template>
  </Swiper>
</template>

<script>
import { Swiper, SwiperItem } from "components/common/swiper";
export default {
  name: "HomeSwiper",
  components: {
    Swiper,
    SwiperItem,
  },
  props: {
    banners: {
      type: Array,
      default() {
        return [
          "https://pic.maizuo.com/usr/2020/108bffa1a9b46189888ba0323d15882e.jpg?x-oss-process=image/quality,Q_70",
          "https://static.maizuo.com/v5/upload/1dab5b8e69fd2ac4319330517d356408.jpg",
          "https://static.maizuo.com/v5/upload/189bcf606b4bf49ad5de201a2ea5024d.jpg?x-oss-process=image/quality,Q_70",
        ];
      },
    },
  },
  data: function () {
    return {};
  },
};
</script>

<style>
</style>