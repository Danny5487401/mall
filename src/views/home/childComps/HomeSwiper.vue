<template>
  <Swiper>
    <template>
      <SwiperItem>
        <template>
          <a>
            <img
              src="https://static.maizuo.com/v5/upload/189bcf606b4bf49ad5de201a2ea5024d.jpg?x-oss-process=image/quality,Q_70"
              alt
            />
          </a>
        </template>
      </SwiperItem>
      <SwiperItem>
        <template>
          <a>
            <img src="https://static.maizuo.com/v5/upload/1dab5b8e69fd2ac4319330517d356408.jpg" alt />
          </a>
        </template>
      </SwiperItem>
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
};
</script>

<style>
</style>