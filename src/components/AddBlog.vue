<template>
<div id="add-blog">
  <h2>添加博客</h2>
  <form v-if="!submited" method="post">
    <label>博客标题</label>
    <input type="text" required v-model="blog.title">
    <label>博客内容</label>
    <textarea v-model="blog.content"></textarea>
    <div id="checkboxes">
      <label>Vue.js</label>
      <input type="checkbox" value="Vue.js" v-model="blog.categories">
      <label>Node.js</label>
      <input type="checkbox" value="Node.js" v-model="blog.categories">
      <label>React.js</label>
      <input type="checkbox" value="React.js" v-model="blog.categories">
      <label>Angular.js</label>
      <input type="checkbox" value="Angular.js" v-model="blog.categories">
    </div>
    <label>作者：</label>
    <select v-model="blog.author">
      <option v-for="author in authors">{{author}}</option>
    </select>
    <button type="button" @click.prevent="post">添加博客</button>
  </form>
  <!-- <hr v-if="!submited"> -->
  <div v-if="submited">
    <h3>您的博客发布成功！</h3>
  </div>
  <div id="preview">
    <h3>博客总览</h3>
    <p>博客标题：{{blog.title}}</p>
    <p>博客内容:</p>
    <p>{{blog.content}}</p>
    <p>博客分类：</p>
    <ul>
      <li v-for="category in blog.categories">
        {{category}}
      </li>
    </ul>
    <p>作者：{{blog.author}}</p>
  </div>
</div>
</template>

<script>
import myaxios from '../myaxios'
export default {
  name: 'add-blog',
  data() {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: ""
      },
      authors: ["hyc", "Vistor"],
      submited: false
    }
  },
  methods: {
    post: function() {
      myaxios.post("", this.blog).then(() => {
        this.submited = true;

      }).then(() => {
        setTimeout(() => {
          this.$router.push('/')
        }, 3000);
      })
    }
  }
}
</script>

<style scoped>
#add-blog * {
  box-sizing: border-box;
  font-family: "微软雅黑";
}

#add-blog {
  margin: 20px auto;
  max-width: 600px;
  padding: 20px;
}

label {
  display: block;
  margin: 20px 0 10px;
}

input[type="text"],
textarea,
select {
  display: block;
  width: 100%;
  padding: 8px;
}

textarea {
  height: 200px;
}

select {
  height: 25px;
  font-size: 16px;
  padding: 0 10px;
}

#checkboxes label {
  display: inline-block;
  margin-top: 0;
}

#checkboxes input {
  display: inline-block;
  margin-right: 10px;
}

button {
  display: block;
  margin: 20px 0;
  background: crimson;
  color: #fff;
  border: 0;
  padding: 14px;
  border-radius: 4px;
  font-size: 18px;
  cursor: pointer;
}

#preview {
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}

h3 {
  margin-top: 10px;

}
</style>
