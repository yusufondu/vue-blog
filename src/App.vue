<template>
  <div id="app">
    <Header />
    <router-view></router-view>
  </div>
</template>

<script>
// import addBlog from "./components/addBlog.vue";
// import showBlog from "./components/showBlog.vue";
// import listBlogs from "./components/listBlogs.vue";
import Header from "./components/Header.vue";

export default {
  name: "App",
  components: {
    // addBlog,
    // showBlog,
    // listBlogs,
    Header,
  },
  data() {
    return {};
  },
  methods: {},
};
</script>

<style scoped>
#app {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  min-height: 100%;
}
</style>
