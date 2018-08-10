<template>
  <div class="about">
    <h1>This is an about page</h1>
    <!-- <button v-on:click="getPost()">Get posts</button> -->
    <div class="ui page dimmer"></div>
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
    <div class="ui modal">
      <i class="close icon"></i>
      <div class="header">
        Modal Title
      </div>
      <div class="image content">
        <div class="image">
          An image can appear on left or an icon
        </div>
        <div class="description">
          A description can appear on the right
        </div>
      </div>
      <div class="actions">
        <div class="ui button">Cancel</div>
        <div class="ui button">OK</div>
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
    this.$Progress.start();
    $('.page.dimmer').dimmer('show');
    axios.get(`http://jsonplaceholder.typicode.com/posts`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.$Progress.finish();
      $('.page.dimmer').dimmer('hide');
      this.posts = response.data.slice(0,10)
    })
    .catch(e => {
      this.errors.push(e)
    })
    // }
  },
  mounted: function(){
    $('.ui.modal')
    .modal()
    ;
  }
}
</script>
