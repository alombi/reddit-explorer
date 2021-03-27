<template>
	<h1>Browse <span @click="changeSub" id="subreddit">r/{{sub}}</span></h1>
</template>


<script>
	export default {
		name:"Title",
		props: {
			sub: String
		},
		methods: {
			changeSub() {
				var newSub = window.prompt('Choose a different subreddit');
				this.$emit('changeSub', newSub)
			},
		},
	}
</script>

<style>
	h1{
		padding-top: 50px;
		text-align: center;
		font-weight: 800;
	}
	#subreddit{
		color:#F09D51;
	}
	@media(prefers-color-scheme:dark){
		h1{
			color:white;
		}
	}
</style>