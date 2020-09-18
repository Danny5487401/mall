<template>
  <div id="profile">
    <nav-bar class="home-nav">
      <template v-slot:center>
        <div>个人信息</div>
      </template>
    </nav-bar>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
export default {
  name: "Profile",
  components: {
    NavBar,
  },
};
</script>

<style>
</style>