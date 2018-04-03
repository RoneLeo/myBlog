<template>
  <div id="addblog">
  	<h1>添加博客</h1>
  	<form action="" v-if="!submmited">
  		<label for="">博客标题</label>
  		<input type="text" v-model="blog.title" required>
  		<label for="">博客内容</label>
  		<textarea name="" v-model="blog.content" id="" rows="10"></textarea>
  		<div id="checkboxes">
  			<label for="">Vue.js</label>
  			<input type="checkbox" value="Vue.js" v-model="blog.categories">
  			<label for="">React.js</label>
  			<input type="checkbox" value="React.js" v-model="blog.categories">
  			<label for="">Angular4.js</label>
  			<input type="checkbox" value="Angular4.js" v-model="blog.categories">
  			<label for="">Node.js</label>
  			<input type="checkbox" value="Node.js" v-model="blog.categories">
  		</div>
  		<label for="">作者：</label>
  		<select name="" id="" v-model="blog.author">
  			<option v-for="author in authors">{{author}}</option>
  		</select>
  		<button v-on:click.prevent="post">添加博客</button>
  	</form>
  	<div v-if="submmited">
  		<h3>您的博客发送成功</h3>
  	</div>
  	<div id="preview">
  		<h3>博客预览</h3>
  		<p>博客标题：{{blog.title}}</p>
  		<p>博客内容：</p>
  		<p>{{blog.content}}</p>
  		<p>博客分类：</p>
  		<ul>
  			<li v-for="category in blog.categories">{{category}}</li>
  		</ul>
  		<p>作者：{{blog.author}}</p>
  	</div>
  </div>
</template>

<script>
// import axios from 'axios'
import axios from '../axios-auth'
export default {
  name: 'AddBlog',
  data () {
    return {
      blog: {
      	title: "",
      	content: "",
      	categories:[],
      	author: ""
      },
      authors: ["Henry", "Rone", "Jery"],
      submmited:false
    }
  },
  methods: {
  	post: function() {
  		// this.$http.post('https://wd1182543348jfzvtq.wilddogio.com/posts.json', this.blog
  		axios.post('https://wd1182543348jfzvtq.wilddogio.com/posts.json', this.blog
  			// this.$http.post('https://jsonplaceholder.typicode.com/posts',{
  			// title:this.blog.title,
  			// content: this.blog.content,
  			// userId: 1
  		).then((data) => {
  			// console.log(data);
  			this.submmited = true;
  		});
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#addblog * {
	box-sizing: border-box;;
}
#addblog {
	margin: 20px auto;
	max-width: 600px;
	padding: 20px;
}
label {
	display: block;
	margin: 20px 0 10px;
}
input[type="text"], textarea, select {
	display: block;;
	width: 100%;
	padding: 8px;
}
select {
	list-style-type: none;
}
textarea {
	height: 200px;
}
#checkboxes label {
	display: inline-block;
	margin-top: 0px;
}
#checkboxes input {
	display: inline-block;
	margin-right: 10px;
}
button {
	display: block;
	margin: 20px 0;
	background-color: crimson;
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
	margin: 30px 0px;
}
h3 {
	margin-top: 10px;
}

</style>
