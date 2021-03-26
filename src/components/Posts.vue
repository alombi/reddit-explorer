<template>
	<h3 id="loader" v-if="loading">Loading...</h3>
	<div class="list">
		<div class="item" v-for="post in posts" :key="post.data.name" @click="()=>openPost(post)">
			<h3>{{ post.data.title }}</h3>
			<img :src="post.data.url" />
		</div>
	</div>
</template>

<script>
	export default {
		name:"Posts",
		props:{
			posts: Array,
			loading: Boolean
		},
		components: {
		},
		methods:{
			openPost(post){
				window.open('https://reddit.com' + post.data.permalink, '_blank');
			}
		},
		data: function() {
			return {
				loader: true,
			}
		},
	}
</script>

<style>
	.list{
		display:grid;
		grid-template-columns: repeat(3, 3fr);
		
	}
	img{
		height:300px;
		width:auto;
		max-width:300px;
	}
	.item{
		background-color: #f1f0f5;
		border-radius: 9px;
		margin:20px;
		text-align: center;
		padding: 15px
	}
	#loader{
		text-align: center;
		padding-top:150px;
	}
	@media(max-width:1000px){
		.list{
			grid-template-columns: 1fr
		}
	}
	@media(prefers-color-scheme:dark){
		.item{
			background-color: #2C2C2E;
			color:white;
		}
	}
</style>