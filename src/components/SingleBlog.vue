<template>
	<div id="single-blog">
		<h1>{{blog.title}}</h1>
		<article>{{blog.content}}</article>
		<!-- <p class="author">作者： {{blog.author}}</p>
		<p class="category">分类：
			<span v-for="category in blog.categories">{{category}}</span>
		</p> -->
		<button v-on:click="deleteSingleBlog()">删除</button>
		<router-link :to="'/edit/' + id"> 
			<button>编辑 </button>
		</router-link>
		<!-- <ul>
			<li v-for="category in blog.categories">{{category}}</li>
		</ul> -->
	</div>
</template>
<script>
import axios from '../axios-auth'
// import axios from 'axios'
	export default{
		name: "single-blog",
		data() {
			return {
				id: this.$route.params.id,
				blog:{

				}
			}
		},
		created() {
			// this.$http.get('https://wd1182543348jfzvtq.wilddogio.com/posts/' + this.id + ".json")
			axios.get('/posts/' + this.id + ".json")
			// .then(function(data) {
			// 	console.log(data);
			// 	// this.blog = data.body;
			// 	return data.json();
			// })
			.then((data) => {
				this.blog = data.data;
			})
		},
		methods: {
			deleteSingleBlog: function() {
				// this.$http.delete("https://wd1182543348jfzvtq.wilddogio.com/posts/" + this.id + ".json")
				axios.delete("/posts/" + this.id + ".json")
				.then(response => {
					this.$router.push({path:"/"})
				})
			}
		}
	}
</script>
<style scoped>
#single-blog {
	max-width: 960px;
	margin: 0 auto;
	padding: 20px;
	background: #eee;
	border: 1px dotted #aaa;
	padding-bottom: 60px;
}
p,span {
	display: inline-block;
}
.author{
	margin-right: 40px;
	float: left;
}
.category {
	float: right;
}
/*span {
	margin-left: 0px;
}
li {
	list-style-type: none;
}*/
</style>