<template>
  <Nav :sub="sub" @sort="refreshSorted" @askRefresh="refresh" />
  <Title :sub="sub" @changeSub="refresh" />
  <Suggestions :sub="sub"  @changeSub="refresh" />
  <Posts :posts="posts" :loading="loading" />
</template>

<script>
  import Title from './components/Title';
  import Posts from './components/Posts';
  import Nav from './components/Nav';
  import Suggestions from './components/Suggestions';
  export default {
    name: 'App',
    components: {
      Title,
      Posts,
      Nav,
      Suggestions,
    },
    methods: {
      refresh(newSub){
        this.loading = true;
        if(newSub != null){
          this.posts = [];
          this.sub = newSub
          fetch(`https://www.reddit.com/r/${newSub}/hot.json?limit=100`)
          .then((response) =>{
            response = response.json()
            return response
          })
          .then((data)=>{
            this.posts = data.data.children
            this.loading = false;
          })
          .catch(()=>{
            console.log('Subreddit not found. ')
            this.loading = false;
            window.alert('Subreddit not found!')
          })
        }
      },
      refreshSorted(sorting){
        this.loading = true;
        this.posts = [];
        fetch(`https://www.reddit.com/r/${this.sub}/${sorting}.json?limit=100`)
        .then((response) =>{
          response = response.json()
          return response
        })
        .then((data)=>{
          this.posts = data.data.children
          this.loading = false;
        })
        .catch((err)=>{
          console.log('Subreddit not found. ', err)
          window.alert('Subreddit not found!')
          this.loading = false;
        })
      }
    },
    mounted() {
      fetch(`https://www.reddit.com/r/dankmemes/hot.json?limit=100`)
      .then((response) =>{
        response = response.json()
        return response
      })
      .then((data)=>{
        this.posts = data.data.children
        this.loading = false;
      })
    },
    data: function() {
      return {
        sub: 'dankmemes',
        posts: [],
        loading: true,
      }
    },
  }
</script>

<style>
  body{
    font-family:  -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    margin:0px;
  }
  @media(prefers-color-scheme:dark){
    body{
      background-color: #1C1C1E;
    }
  }
</style>