<template>
  <div v-theme:column="'wide'" id="show-blogs">
    <h1>All Blog Articles</h1>
    <input type="text" v-model="search" placeholder="Search Blogs" />
    <div v-for="blog in filteredBlogs" :key="blog.id" class="single-blog">
      <router-link :to="'/blog/' + blog.id">
        <h2 v-rainbow>{{ blog.title | capitalize }}</h2>
      </router-link>
      <article>{{ blog.content | snippet }}</article>
    </div>
  </div>
</template>

<script>
import searchMixin from "../mixins/searchMixin";

export default {
  data() {
    return {
      blogs: [],
      search: "",
    };
  },
  methods: {},
  created() {
    // console.log("route:", this.$route.params);
    this.$http
      .get("https://vue2-blog-project-default-rtdb.firebaseio.com/posts.json")
      .then(function (data) {
        return data.json();
      })
      .then(function (data) {
        // console.log(data);
        let blogsArray = [];
        for (let key in data) {
          data[key].id = key;
          blogsArray.push(data[key]);
        }
        this.blogs = blogsArray;
      });
  },
  computed: {},
  filters: {
    capitalize: function (value) {
      return value.toUpperCase();
    },
    snippet: function (value) {
      return value.slice(0, 100) + "...";
    },
  },
  directives: {
    rainbow: {
      bind(el) {
        el.style.color = "#" + Math.random().toString(16).slice(2, 8);
      },
    },
    theme: {
      bind(el, binding) {
        if (binding.value == "wide") {
          el.style.maxWidth = "1200px";
        } else if (binding.value == "narrow") {
          el.style.maxWidth = "560px";
        }
        if (binding.arg == "column") {
          el.style.background = "#ddd";
          el.style.padding = "20px";
        }
      },
    },
  },
  mixins: [searchMixin],
};
</script>

<style scoped>
#show-blogs {
  max-width: 800px;
  margin: 0 auto;
}
.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
}
</style>
