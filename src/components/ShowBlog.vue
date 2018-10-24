<template>
<div id="show-blog">
  <h1>博客总览</h1>
  <input type="text" placeholder="search blogs" v-model='search'>
  <div id="single-blog" v-for="blog in filterBlog">
    <router-link :to="'/blog/'+blog.objectId">
      <h2 v-changecolor>{{blog.title | toUpcase}}</h2>
    </router-link>
    <article>
      {{blog.content | snippet}}
    </article>
    <!-- <a href="javascript:;" class="fa fa-trash-o" @click=deleteblog></a> -->
  </div>
</div>
</template>

<script>
import myaxios from '../myaxios'
export default {
  name: 'show-blog',
  data() {
    return {
      blogs: [],
      search: ''
    }
  },
  created() {
    myaxios.get("").then((data) => {
      return data.data.results
    }).then((res) => {
      for (let key in res) {
        //     console.log(key);
        //     console.log(res[key]);
        res[key].id = key;
        this.blogs.push(res[key]);
        // console.log(this.blogs[key].objectId);
      }
    })
  },
  // methods:{
  //   deleteblog:function(){
  //     this.$http.delete("https://hycwebprogram1.firebaseio.com/posts/"+'-LP-vkldraUnfl5xUVCP').then((res)=>{
  //       console.log(res);
  //     })
  //   }
  // },
  computed: {
    filterBlog: function() {
      return this.blogs.filter((blog) => {
        return blog.title.match(this.search)
      })
    }
  },
  filters: {
    'toUpcase': function(value) {
      return value.toUpperCase();
    }
  },
  directives: {
    changecolor: {
      bind(el, binding, vnode) {
        el.style.color = '#' + Math.random().toString(16).slice(2, 8);
      }
    }
  }
}
</script>

<style scoped>
#show-blog {
  max-width: 800px;
  margin: 0 auto;
}

#single-blog {
  padding: 20px;
  margin: 20px 0;
  background: #eee;
  box-sizing: border-box;
  border: 1px solid #aaa;
}

#single-blog a {
  color: #444;
  text-decoration: none;
}

input {
  width: 100%;
  height: 30px;
  border-radius: 5px;
  font-size: 18px;
  box-sizing: border-box;
}
</style>
