<template>
  <div>
    <SearchHotspot />
    <swiper indicator-dots autoplay>
      <block v-for="item in swiperdata" :key="item.goods_id">
        <swiper-item>
          <image :src="item.image_src" />
        </swiper-item>
      </block>
    </swiper>
    <div class="category">
      <div v-for="item in catitems" :key="item.name">
        <image :src="item.image_src" />
      </div>
    </div>
    <div class="floor" v-for="(item,index) in floordata" :key="index">
      <div class="title">
        <img :src="item.floor_title.image_src" />
      </div>
      <div class="btm-box">
        <img :src="item.product_list[0].image_src" />
        <div class="right">
          <block v-for="(item2, index2) in item.product_list" :key="index2">
            <img v-if="index2" :src="item2.image_src" />
          </block>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SearchHotspot from "@/components/SearchHotspot";
export default {
  components: {
    SearchHotspot
  },
  data() {
    return {
      swiperdata: [],
      catitems: [],
      floordata: []
    };
  },
  created() {
    this.getSwiperdata();
    this.getCatitems();
    this.getFloordata();
  },
  methods: {
    getSwiperdata() {
      this.$request({
        url: "/api/public/v1/home/swiperdata"
      }).then(data => {
        this.swiperdata = data;
      });
    },
    getCatitems() {
      this.$request({
        url: "/api/public/v1/home/catitems"
      }).then(data => {
        this.catitems = data;
      });
    },
    getFloordata() {
      this.$request({
        url: "/api/public/v1/home/floordata"
      }).then(data => {
        this.floordata = data;
      });
    }
  }
};
</script>

<style lang="less">
.search {
  background-color: #eb4450;
  padding: 0 16rpx 20rpx;
  input {
    color: #bbb;
    height: 60rpx;
    background-color: #fff;
    border-radius: 4rpx;
    text-align: center;
  }
}
swiper {
  height: 340rpx;
  image {
    width: 100%;
    height: 100%;
  }
}
.category {
  height: 194rpx;
  display: flex;
  justify-content: space-around;
  align-items: center;
  image {
    width: 128rpx;
    height: 140rpx;
  }
}
.floor {
  .title {
    width: 100%;
    height: 88rpx;
    background-color: #f4f4f4;
    position: relative;
    img {
      width: 100%;
      height: 60rpx;
      position: absolute;
      left: 0;
      bottom: 0;
    }
  }
  .btm-box {
    display: flex;
    padding: 20rpx 17rpx;
    > img {
      width: 232rpx;
      height: 386rpx;
    }
    .right {
      flex: 1;
      display: flex;
      flex-wrap: wrap;
      img {
        width: 232rpx;
        margin-left: 10rpx;
        margin-bottom: 10rpx;
        height: 188rpx;
      }
    }
  }
}
</style>