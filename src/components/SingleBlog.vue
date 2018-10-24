<template>
<div id="single-blog">
  <h1>{{blog.title}}</h1>
  <p>博客内容：</p>
  <article>
    {{blog.content}}
  </article>
  <p>作者：<span>{{blog.author}}</span></p>
  <p>分类：</p>
  <ul>
    <li v-for="item in blog.categories">
      {{item}}
    </li>
  </ul>
</div>
</template>

<script>
import myaxios from '../myaxios'
export default {
  name: 'single-blog',
  data() {
    return {
      id: this.$route.params.id,
      blog: {}
    }
  },
  created() {
    myaxios.get("https://glgkkyip.api.lncld.net/1.1/classes/blog/" + this.id).then((res) => {
        return res.data
        // console.log(this.id.id);
        // console.log(data);
      })
      .then((res) => {
        this.blog = res;
      })
  }
}
</script>

<style scoped>
#single-blog {
  max-width: 960px;
  margin: 0 auto;
  padding: 20px;
  background: #eee;
  border: 1px solid #aaa;
}

ul {
  list-style: none;
}

p {
  font-weight: bold;
}
</style>
