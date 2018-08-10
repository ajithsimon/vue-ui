<template>
  <div class="home">
    <h2>Home Page</h2>
    <div class="ui dimmer">
      <div class="ui loader"></div>
    </div>
    <div v-if="studioData" class="ui grid container">
      <div class="two column row">
        <div class="ui card column">
          <div class="content">
            <div class="header">{{studioData.title }}</div>
            <div class="description">
              <p>{{studioData.description}}</p>
              <p>Director: {{studioData.director}}, Producer: {{studioData.producer}}</p>
              <p>Released at:{{studioData.released_date}}, IMDB: {{studioData.rt_score}}%</p>
            </div>
            <div class="description">
              <p v-for="artist in artists">  {{artist.name}}<img src="https://source.unsplash.com/collection/190727/1600x900" alt="img" width="200px"/></p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'home',
  data(){
    return{
      studioData:[],
      artists:[],
      errors:[]
    }
  },
  created() {
    this.$Progress.start();
    $('.ui.dimmer').dimmer('show');
    axios.get(`https://ghibliapi.herokuapp.com/films/58611129-2dbc-4a81-a72f-77ddfc1b1b49`)
    .then(response => {
      $('.ui.dimmer').dimmer('hide');
      this.studioData = response.data;
      this.people = this.studioData.people;
      for(var i=0;i<this.people.length;i++){
        axios.get(this.people[i])
        .then(response => {
          this.$Progress.finish();
          this.artists.push(response.data);
        })
      }
    })
    .catch(e => {
      this.errors.push(e)
    })

    //unsplash
    axios.get('https://source.unsplash.com/random')
    .then(response => {
      console.log(response.data);
    })
  }
}
</script>
