<template>
  <div class="banner-city">
    <router-link :to="{path:'/search'}" class="city-search">
      <v-search></v-search>
    </router-link>
    <div class="city-scroll">
      <swiper :options="swiperOption" ref="mySwiper">
        <swiper-slide v-for="item in data.data?data.data.data[0] : []">
          <router-link :to="{path: '/banner/' + item.reference_id }">
            <img class="banner-img" :src="item.ad_pic_url" />
          </router-link>
        </swiper-slide>
      </swiper>
    </div>
    <!--导航-->
    <ul class="city-nav">
      <li v-for="(item,index) in navArr" @click="navGo(index,item.id)">
        <span :class="item.icon"></span> 
        <label>{{item.name}}</label>
      </li>
    </ul>
  </div>
</template>

<script>
  import {
    mapActions,
    mapGetters
  } from 'vuex'
  import types from 'types'
  import richSwiper from 'components/common/richSwiper'
  import Search from 'components/common/search'
  import { swiper, swiperSlide } from 'vue-awesome-swiper'
  export default {
    components: {
      //搜索
      "v-search": Search,
      //滑动
      "v-swiper": richSwiper,
      swiper,
      swiperSlide
    },
    data() {
      return {
        swiperOption: {
          autoplay: 5000,
          initialSlide: 1,
          loop: true
        },
        banner: {
          swiper: false,
          box: 3,
          autoplay: 4,
        },
        navArr: [{
            icon: "c-free",
            name: "免费",
            id: 371
          },
          {
            icon: "c-girl",
            name: "女生",
            id: 370
          },
          {
            icon: "c-boy",
            name: "男生",
            id: 369
          },
          {
            icon: "c-classfy",
            name: "分类"
          },
          {
            icon: "c-rank",
            name: "排行"
          }
        ],
      }
    },
    props: {
      data: {
        type: Object,
        default () {
          return {};
        }
      }
    },
    methods: {
      navGo(i, id) {
          if(i === 0){
            this.$router.push({path: '/free'})
          }else if(i >= 1 && i <= 2) {
            this.$router.push({path: '/containertwo/'+id})
          } else if (i == 3) {
            this.$router.push({path: 'category'});
          } else if (i == 4) {
            this.$router.push({path: 'ranks'})
          };
      }
    }
  }
</script>
<style lang="scss">
.banner-img{
  width: 100%;
}
</style>