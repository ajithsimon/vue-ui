<template>
  <div class="about">
    <h1>This is an about page</h1>
    <!-- <button v-on:click="getPost()">Get posts</button> -->
    <div v-if="posts && posts.length" class="ui grid">
      <div class="five column row">
        <div class="column" v-for="post in posts">
          <div class="ui card">
            <div class="content">
              <div class="header">{{post.title | truncate(40)}}</div>
              <div class="meta">2 days ago</div>
              <div class="description">
                <p>{{post.body | truncate(100)}}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios';
export default{
  name: 'about',
  data(){
    return{
      posts: [],
      errors: []
    }
  },
  created() {
    // getPost: function() {
      this.$Progress.start()
      axios.get(`http://jsonplaceholder.typicode.com/posts`)
      .then(response => {
        // JSON responses are automatically parsed.
        this.$Progress.finish()
        this.posts = response.data.slice(0,10)
      })
      .catch(e => {
        this.errors.push(e)
      })
    // }
  }
}
</script>
