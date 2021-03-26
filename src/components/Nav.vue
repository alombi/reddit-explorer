<template>
	<div class="navbar">
		<div id="left">
			<h3 @click="scrollToTop">r/{{ sub }}</h3>
		</div>
		<div id="right">
			<a @click="sortPerNew">Sort per {{sort}}</a>
			<a href="">GitHub</a>
		</div>
	</div>
</template>

<script>
	export default {
		name:"Nav",
		props:{
			sub:String
		},
		methods:{
			scrollToTop(){
				window.scrollTo(0, 0)
			},
			sortPerNew(){
				this.$emit('sortPerNew')
				this.sort = 'hot'
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
		padding:10px;
		color:white;
		text-decoration: none;
		border-radius:30px;
		font-size: 13px
	}
	#left > h3{
		font-size:22px;
		color:white;
		font-weight: 500;
	}
</style>