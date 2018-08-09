<template>
  <div class="home">
    <h2>Home Page</h2>
    <div v-if="studioData" class="ui grid">
      <div class="five column row">
        <div class="column">
          <div class="ui card">
            <div class="content">
              <div class="header">{{studioData.title }}</div>
              <div class="description">
                <p>{{studioData.description}}</p>
                <p>Director: {{studioData.director}}, Producer: {{studioData.producer}}</p>
                <p>Released at:{{studioData.released_date}}, IMDB: {{studioData.rt_score}}%</p>
              </div>
              <div class="description">
                {{studioData.people}}
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
export default {
  name: 'home',
  data(){
    return{
      studioData:[],
      people:[],
      errors:[]
    }
  },
  created() {
    this.$Progress.start()
    axios.get(`https://ghibliapi.herokuapp.com/films/58611129-2dbc-4a81-a72f-77ddfc1b1b49`)
    .then(response => {
      this.$Progress.finish()
      this.studioData = response.data;
      this.people = studioData.people;
      // console.log(response.data);
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>
