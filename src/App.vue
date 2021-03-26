<template>
  <Nav :sub="sub" @sortPerNew="refreshSorted" />
  <Title :sub="sub" @changeSub="refresh" />
  <Posts :posts="posts" />
</template>

<script>
  import Title from './components/Title';
  import Posts from './components/Posts';
  import Nav from './components/Nav';
  export default {
    name: 'App',
    components: {
      Title,
      Posts,
      Nav,
    },
    methods: {
      refresh(newSub){
        if(newSub != null){
          fetch(`https://www.reddit.com/r/${newSub}/hot.json?limit=100`)
          .then((response) =>{
            response = response.json()
            return response
          })
          .then((data)=>{
            this.posts = data.data.children
            this.sub = newSub
          })
          .catch((err)=>{
            console.log('Subreddit not found. ', err)
            window.alert('Subreddit not found!')
          })
        }
      },
      refreshSorted(){
        fetch(`https://www.reddit.com/r/${this.sub}/new.json?limit=100`)
        .then((response) =>{
          response = response.json()
          return response
        })
        .then((data)=>{
          this.posts = data.data.children
        })
        .catch((err)=>{
          console.log('Subreddit not found. ', err)
          window.alert('Subreddit not found!')
        })
      }
    },
    mounted() {
      fetch(`https://www.reddit.com/r/memes/hot.json?limit=100`)
      .then((response) =>{
        response = response.json()
        return response
      })
      .then((data)=>{
        this.posts = data.data.children
      })
    },
    data: function() {
      return {
        sub: 'memes',
        posts : []
      }
    },
  }
</script>

<style>
  body{
    font-family:  -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    margin:0px;
  }
</style>
