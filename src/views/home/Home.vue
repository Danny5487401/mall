<template>
  <div id="home">
    <nav-bar class="home-nav">
      <template v-slot:center>
        <div>电影节</div>
      </template>
    </nav-bar>
    <div class="content">
      <HomeSwiper :banners="banners"></HomeSwiper>
    </div>
  </div>
</template>


<script>
import HomeSwiper from "./childComps/HomeSwiper";

import NavBar from "components/common/navbar/NavBar";

import {getHomeMultidata} from 'network/home'

export default {
  name: "home",
  components: {
    HomeSwiper,
    NavBar,
  },
  created(){
    //1.获取首页多个数据
    this.getHomeMultidata()
    
  },
  data(){
    return {
      banners:[],
      recommends:[],
    }
  },
  methods:{
    getHomeMultidata (){
      getHomeMultidata().then(res => {
          console.log(res)
          this.banners = res.data.banner.list;
          this.recommends = res.data.recommend.list;
    }
  )
    }}
};
</script>

<style>
.home-nav {
  background-color: var(--color-tint);
  color: #fff;

  /*在使用浏览器原生滚动时, 为了让导航不跟随一起滚动*/
  /* position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9; */
}
.content {
  overflow: hidden;

  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
}
</style>