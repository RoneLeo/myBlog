<template>
  <div v-theme:column="'narrow'" id="showblogs">
  	<h1>博客总览</h1>
  	<input type="text" v-model="search" placeholder="搜索">
  	<div class="single-blog" v-for="blog in filteredBlogs" :key="blog.title">
  		<router-link v-bind:to="'/blog/' + blog.id">
  			<h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
  			<article>{{blog.content | snippet}}</article>
  		</router-link>
   </div>
  </div>
</template>

<script>

// import axios from '../axios-auth'
import axios from '../axios-auth'
export default {
  name: 'ShowBlogs',
  data () {
  	return {
  		blogs:[],
  		search: ""

  	}
  },
  created() {
  	// this.$http.get('https://wd1182543348jfzvtq.wilddogio.com/posts.json')
  	axios.get('https://wd1182543348jfzvtq.wilddogio.com/posts.json')
  	.then(function(data) {
  		// console.log(data.json());
  		// return data.json();
  		//this.blogs = data.body.slice(0,10);
  		// console.log(data);
  		return data.data;
  	}).then((data) => {
  		var blogsArray = [];
  		for(let key in data) {
  			// console.log(key);
  			data[key].id = key;
  			blogsArray.push(data[key]);
  		}
  		// console.log(blogsArray);
  		this.blogs = blogsArray;
  	});
  },
  computed: {
  	filteredBlogs: function() {
  		return this.blogs.filter((blog) => {
  			return blog.title.match(this.search);
  		})
  	}
  },
  //组件局部过滤器
  filters: {
  	"to-uppercase": function(value) {
  		return value.toUpperCase();
  	},
  	"snippet": function(value) {
  		return value.slice(0,100) + "...";
  	}
  	// toUpperCase(value) {
  	// 	return value.toUpperCase();
  	// }
  },
  //组件局部自定义指令
  directives: {
  	'rainbow': {
  		bind(el, binding, vcode) {
  			el.style.color = "#" + Math.random().toString(16).slice(2,8);
  		}
  	}
  }
}
</script>

<style>
#showblogs {
	max-width: 800px;
	margin: 0 auto;
}
.single-blog {
	padding: 20px;
	margin: 20px 0;
	box-sizing:  border-box;
	background: #eee;
	border: 1px dotted #aaa;
}
a {
	color: #444;
	text-decoration: none;
}
input[type="text"] {
	padding: 8px;
	width: 100%;
	box-sizing: border-box;

}
</style>
