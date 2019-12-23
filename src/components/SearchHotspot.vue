<template>
  <div class="search">
    <div class="input">
      <icon type="search" size="18" color="#bbb"></icon>搜索
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  }
};
</script>

<style lang="less">
.search {
  background-color: #eb4450;
  padding: 0 16rpx 20rpx;
  .input {
    color: #bbb;
    height: 60rpx;
    background-color: #fff;
    border-radius: 4rpx;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>