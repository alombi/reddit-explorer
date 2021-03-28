<template>
	<div>
		<a id="memes" @click="chooseSuggestion">memes</a>
		<a id="dankmemes" @click="chooseSuggestion">dankmemes</a>
		<a id="meme" @click="chooseSuggestion">meme</a>
		<a id="vexillology" @click="chooseSuggestion">vexillology</a>
		<a id="amoledbackgrounds" @click="chooseSuggestion">amoledbackgrounds</a>
		<a id="programmerhumor" @click="chooseSuggestion">programmerhumor</a>
		<!-- <a id="macsetups" @click="chooseSuggestion">macsetups</a> -->
	</div>
</template>


<script>
	export default {
		name: 'Suggestions',
		props:{
			sub: String,
		},
		methods: {
			chooseSuggestion(e) {
				var newSub = e.target.childNodes[0].data
				this.$emit('changeSub', newSub)
			},
		},
		mounted() {
			var active = document.getElementById(this.sub)
			active.classList.add('active')
		},
		watch:{
			sub:function(){
				try{
					document.getElementsByClassName('active')[0].classList.remove('active')
					var active = document.getElementById(this.sub)
					if(active != null){
						active.classList.add('active')
					}
				}catch{
					console.log('No activee')
				}
			}
		}
	}
</script>

<style scoped>
	.active{
		background-color: #F09D51;
	}
	div{
		margin: auto;
		text-align: center;
		display: flex;
		flex-wrap:wrap;
		justify-content:center;
	}
	a{
		background-color: red;
		margin-right:10px;
		padding:5px;
		border-radius: 20px;
		background-color: #F06543;
		margin-top:10px;
		color:white;
	}
</style>