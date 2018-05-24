<template>
  <div class="dashboard">
    <nav class="navbar navbar-dark bg-dark">
      <a class="navbar-brand" href="#">
        <img src="https://a.storyblok.com/f/39898/1024x1024/dea4e1b62d/vue-js_logo-svg.png" width="40" height="40">
      </a>
      <div>
        <img :src="$auth.user.picture" width="30" height="30">
        <span class="text-muted font-weight-light px-2">{{$auth.user.name}}</span>
        <button type="button" class="btn btn-outline-secondary btn-sm" @click="$auth.logout()">Logout</button>
      </div>
    </nav>
  
    <div class="jumbotron">
      <div class="container">
        <h1 class="display-4">Hello, {{$auth.user.name}}!</h1>
        <p class="lead">We hope you liked this tutorial and can now start building new astounding projects from this start point. If you're interested in what we're doing besides tech tutorials check out <a href="https://www.storyblok.com">@storyblok</a>.</p>
        <hr class="my-4">
        <p>TBH, I'm sure this project of yours would look great with a landing page filled with content composed in <a href="https://www.storyblok.com">Storyblok</a> 🎉</p>
        
        <p class="lead">
          <a class="btn btn-primary btn-lg mr-2" href="https://www.storyblok.com/getting-started" target="_blank" role="button">Getting Started</a>
          <a class="btn btn-secondary btn-lg" href="https://twitter.com/home?status=Have%20a%20look%20at%20%40storyblok%20and%20their%20%40vuejs%20%2B%20%40auth0%20tutorial%3A%20https%3A//www.storyblok.com/tp/how-to-auth0-vuejs-authentication" target="_blank" role="button">Tweet it</a>
        </p>

      </div>
    </div>

    <div class="container">
      <div class="card-columns">

        <a class="card" :href="getStoryLink(story)" target="_blank" v-for="story in stories">
          <img class="card-img-top" :src="story.content.image" :alt="story.content.image_alt">
          <div class="card-body">
            <h5 class="card-title">{{story.content.title}}</h5>
            <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
          </div>
        </a>
        
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      stories: []
    }
  },
  mounted() {
    axios.get('https://api.storyblok.com/v1/cdn/stories?starts_with=tp&excluding_fields=body&excluding_ids=48471,48547,60491&token=dtONJHwmxhdJOwKxyjlqAgtt').then((res) => {
      this.stories = res.data.stories
    })
  },
  methods: {
    getStoryLink(story) {
      return `https://www.storyblok.com/${story.full_slug}`
    }
  }
}
</script>

<style scoped>
@import url('https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css');

.btn-primary {
  background: #468f65;
  border: 1px solid #468f65;
}
.card {
  text-decoration: none;
  color: #000;
}
</style>
