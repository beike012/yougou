<template>
  <div>
    home
   <input placeholder="最大输入长度为10" />
  </div>
</template>

<script>
export default {
data() {
  return {
    
  }
},
mounted() {
  wx.showLoading({
  title: '加载中',
})

setTimeout(function () {
  wx.hideLoading()
}, 2000)
},
}
</script>

<style>

</style>