<template>
  <HeaderComponent></HeaderComponent>

  <main class="container mt-4">
    <router-view></router-view>
  </main>

</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue';
export default {
  name: "App",
  components: { HeaderComponent },
  data() {
    return {
      title: "vue",

    };
  },

}
</script>

<style lang="scss" scoped>

</style>