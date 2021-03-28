<template>
	<div class="navbar">
		<div id="left">
			<h3 @click="scrollToTop">r/{{ sub }}</h3>
		</div>
		<div id="right">
			<a @click="askRefresh">Refresh</a>
			<a @click="sortPerNew">Sort per {{sort}}</a>
			<a href="https://github.com/alombi/reddit-explorer" target="_blank"><ion-icon name="logo-github"></ion-icon></a>
		</div>
	</div>
</template>

<script>
	export default {
		name:"Nav",
		props:{
			sub: String
		},
		methods:{
			scrollToTop(){
				window.scrollTo(0, 0)
			},
			sortPerNew(){
				if(this.sort == 'new'){
					this.$emit('sort', 'new')
					this.sort = 'hot'
				} else{
					this.$emit('sort', 'hot')
					this.sort = 'new'
				}
			},
			askRefresh(){
				var newSub = document.getElementById('subreddit').innerText.replace('r/', '');
				this.$emit('askRefresh', newSub)
			}
		},
		data:function(){
			return{
				sort:'new'
			}
		}
	}
</script>

<style>
	ion-icon{
		font-size: 16px;
	}
	.navbar{
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding:5px;
		position:fixed;
		top:0;
		width:100%;
		margin: auto;
		background-color:#F06543;
		height: 40px;
	}
	#right{
		display:flex; 
	}
	#right > a{
		margin-left:5px;
		margin-right: 10px;
		background-color:#313638;
		padding:9px;
		color:white;
		text-decoration: none;
		border-radius:30px;
		font-size: 11.5px;
		margin-top:2px;
	}
	#left > h3{
		font-size:19px;
		color:white;
		font-weight: 500;
	}
</style>