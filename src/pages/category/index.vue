<template>
  <div>
    <SearchHotspot />
    <div class="main">
      <div class="left">
        <div
          class="left_items"
          :class="{active:index===idx}"
          v-for="(item,index) in categories"
          :key="index"
          @click="idx=index"
        >{{item.cat_name}}</div>
      </div>
      <div class="right">
        <img src="/static/images/titleimage.png">
        <ul>
          <li class="cate2"
              v-for="(cate2, index2) in categories[idx].children"
              :key="index2">
            <p>/<span>{{cate2.cat_name}}</span>/</p>
            <ul>
              <li class="cate3"
                  v-for="(cate3, index3) in cate2.children"
                  :key="index3">
                <img :src="cate3.cat_icon">
                <span>{{cate3.cat_name}}</span>
              </li>
            </ul>
          </li>
        </ul>
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
      categories: [],
      idx: 0
    };
  },
  created() {
    this.$request({
      url: "/api/public/v1/categories"
    }).then(data => {
      this.categories = data;
    });
  }
};
</script>

<style lang="less">
.main {
  display: flex;
  position: absolute;
  top: 80rpx;
  bottom: 0;
  width: 100%;
  .left {
    width: 198rpx;
    height: 100%;
    overflow: scroll;
    .left_items {
      width: 100%;
      height: 100rpx;
      line-height: 100rpx;
      border-bottom: 1px solid #eee;
      background-color: #f4f4f4;
      color: #333;
      text-align: center;
      &.active {
        color: #eb4450;
        background-color: #fff;
        position: relative;
        &::before {
          content: "";
          position: absolute;
          width: 8rpx;
          height: 60rpx;
          background-color: #eb4450;
          left: 0;
          top: 20rpx;
        }
      }
    }
  }
  .right {
    flex: 1;
  padding: 20rpx 16rpx;
  height: 100%;
  overflow: scroll;
  > img {
    width: 520rpx;
    height: 180rpx;
  }
  .cate2 {
    margin-bottom: 20rpx;
    p {
      color: #e0e0e0;
      height: 110rpx;
      line-height: 110rpx;
      text-align: center;
      span {
        color: #333;
        padding: 0 30rpx;
      }
    }
    ul {
      display: flex;
      flex-wrap: wrap;
    }
  }
  .cate3 {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 33.33%;
    margin-top: 30rpx;
    > img {
      width: 120rpx;
      height: 120rpx;
    }
    span {
      font-size: 24rpx;
    }
  }
}
}
</style>