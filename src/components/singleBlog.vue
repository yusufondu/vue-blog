<template>
  <div id="single-blog">
    <h1>{{ blog.title }}</h1>
    <article>{{ blog.content }}</article>
    <p>Author: {{ blog.author }}</p>
    <ul>
      <li v-for="category in blog.categories" :key="category">
        {{ category }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      id: this.$route.params.id,
      blog: {},
    };
  },
  created() {
    console.log(this.$route);
    this.$http
      .get(
        `https://vue2-blog-project-default-rtdb.firebaseio.com/posts/${this.id}.json`
      )
      .then((data) => {
        return data.json();
      })
      .then(function (data) {
        this.blog = data;
      });
  },
};
</script>

<style scoped>
#single-blog {
  max-width: 960px;
  margin: 0 auto;
}

ul {
  padding: 0;
  margin-left: 0;
  text-align: left;
}

li {
  margin-left: 0;
}
</style>
