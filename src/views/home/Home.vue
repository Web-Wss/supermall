<template>
<div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <swiper>
      <swiper-item v-for="item in banners" :key="item.link">
        <a :href="item.link">
          <img :src="item.image" alt="">
        </a>
      </swiper-item>
    </swiper>
</div>
</template>

<script>

  import NavBar from 'components/common/navbar/NavBar.vue';
  import {getHomeMultidata} from "network/home";
  import {Swiper, SwiperItem} from 'components/common/swiper';

export default {
  name: "Home",
  components: {
    NavBar,
    Swiper,
    SwiperItem
  },
  data() {
    return {
      result: null,
      banners: [],
      recommends: []
    }
  },
  created() {
    // 1、请求多个数据
    getHomeMultidata().then(res => {
      // console.log(res);
      this.result = res;
      this.banners = res.data.data.banner.list;
      this.recommends = res.data.data.recommend.list;
    })
  }
}
</script>

<style scoped>
  .home-nav {
    background-color: var(--color-tint);
    color: white;
  }
</style>