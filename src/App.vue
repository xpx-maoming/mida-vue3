<template>
<div class="page">
  <img alt="Vue logo" src="./assets/封面图_4.jpg">
  <div class="wihetInfor">
    <Information></Information>
  </div>
</div>

</template>

<script>
import Information from './components/Information/Information.vue'
export default {
  name: 'App',
  components: {
    Information
  }
}
</script>
<style lang="less" scoped>
.page{
  width: 750px;
  padding: 0;
  margin: 0 auto;
}
.wihetInfor{
  width: 700px;
  margin: 0 auto;
}
</style>

