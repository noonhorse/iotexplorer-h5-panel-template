<template>
  <div class="panel">
    <div>
      <h2>vue panel demo</h2>
      <img :src="logo" className="logo">
      <van-tabs v-model:active="active" style="margin-bottom: 20px">
        <van-tab title="home" name="/"></van-tab>
        <van-tab title="about" name="/about"></van-tab>
      </van-tabs>

      <router-view></router-view>
    </div>
  </div>
</template>

<script>
// 小图可以用这种方式生成data-url，大图请上传服务器后使用url
import logo from 'data-url:./assets/logo.svg';
import { ref, watch } from 'vue';
import { useRoute, useRouter } from 'vue-router';

export default {
  setup(){
    const route = useRoute();
    const router = useRouter();
    const active = ref('/');
    router.isReady().then(() => {
      active.value = route.path;
    });
    watch(active, (active) => {
      router.push(active);
    });
    return { logo, path: route.path, active, router };
  }
}
</script>

<style lang="less">
@green: green;
h3 {
  color: red;
  font-size: 18px;
}
h1 {
  color: @green;
}
.panel {
  padding: 0 10px;
}
.logo{
  display:block;
  margin: 0 auto;
  width: 100px;
  height: 100px;
  margin-bottom: 10px;
}
</style>
