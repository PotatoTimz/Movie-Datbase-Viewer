<template>
  <div v-if="left">
    <section class = "hero is-dark">
        <div class="columns">
          <div class="column is-4 recTextLeft " id="rec1info">
              <h1 id="title" class="is-clickable" v-on:click="moreInfo()">{{ title }}</h1>
              <p id="info">{{ date }} &emsp;|&emsp; {{ language }} &emsp;|&emsp; {{ runtime }} &emsp;|&emsp; {{ company }}</p>
              <p><strong>Genre:</strong> {{ genre }}</p>
              <br>
              <p>{{ description }}</p>
              <br>
              <p><strong>Director:</strong> {{ director }}</p>
              <p><strong>Writer:</strong> {{ writer }}</p>
              <p><strong>Staring:</strong> {{ star }}</p>
              <br>

              <div class="field is-horizontal" id="ratebars">
                    <div class="field-label">
                        <label><strong>Score</strong></label>
                    </div>
                    <div class="field-body">
                        <div class="field">
                          <svg height="35" width="400">
                            <rect y="0" v-bind:width="score/10*400" height="35" fill="green"/>
                            <text y="25" x ="10" fill="white">{{ score }}</text>
                          </svg>
                        </div>
                    </div>
                </div> 

          </div>

          <div class="column is-3" id="rec1poster">
              <img id="recposter" class="is-clickable" v-bind:src="poster" v-on:click="moreInfo()">
          </div>

          <div class="column" id="rec1photos">
              <img id="photo" v-bind:src="image1">
              <img id="photo" v-bind:src="image2">
              <img id="photo" v-bind:src="image3">
              <img id="photo" v-bind:src="image4">
          </div>
        </div>
    </section>
  </div>
  <div v-else>
      <section class = "hero">
        <div class="columns">
            <div class="column is-3" id="rec2poster">
                <img id="recposter" class="is-clickable" v-bind:src="poster" v-on:click="moreInfo()">
            </div>

            <div class="column is-5" id="rec2photos">
                <img id="photo" v-bind:src="image1">
                <img id="photo" v-bind:src="image2">
                <img id="photo" v-bind:src="image3">
                <img id="photo" v-bind:src="image4">
            </div>

            <div class="column  is-4 recTextRight" id="rec2info">
                <h1 id="title" class="is-clickable" v-on:click="moreInfo()">{{ title }}</h1>
                <p id="info">{{ date }} &emsp;|&emsp; {{ language }} &emsp;|&emsp; {{ runtime }} &emsp;|&emsp; {{ company }}</p>
                <p><strong>Genre:</strong> {{ genre }}</p>
                <br>
                <p>{{ description }}</p>
                <br>
                <p><strong>Director:</strong> {{ director }}</p>
                <p><strong>Writer:</strong> {{ writer }}</p>
                <p><strong>Staring:</strong> {{ star }}</p>
                <br>
                
                <div class="field is-horizontal" id="ratebars2">
                    <div class="field-label">
                        <label><strong>Score:</strong></label>
                    </div>
                    <div class="field-body">
                        <div class="field">
                          <svg height="35" width="400">
                            <rect v-bind:width="score/10*400" height="35" fill="green"/>
                            <text y="25" x ="10" fill="white">{{ score }}</text>
                          </svg>
                        </div>
                    </div>
                </div> 
            </div>

        </div>
      </section>
  </div>

</template>

<script>
  let reccomended = [
      {"id": 8844, "pictures": [1,2, 5, 6]},
      {"id": 4233, "pictures": [3,23, 18, 22]},
      {"id": 603692, "pictures": [3,11, 5, 10]},
      {"id": 299536, "pictures": [39, 44, 6, 43]},
      {"id": 585, "pictures": [4,12, 6, 18]},
      {"id": 4935, "pictures": [4, 5, 6, 11]},
      {"id": 694, "pictures": [4,11, 12, 13]},
      {"id": 19995, "pictures": [4, 5, 6, 10]}, 
      {"id": 1891, "pictures": [7, 18, 33, 44]},
      {"id": 857, "pictures": [24, 25, 26, 23]}
  ];

  export default {
    
    name: 'ReccomendedPage',
    props: {
      id: Number,
      left: Boolean
    },
    data() {
      return {
        title: "",
        date: "",
        language: "",
        runtime: "",
        company : "",
        genre : "",
        description : "",
        director : "",
        writer : "",
        star : "",
        score : "",
        poster : "",
        image1 : "",
        image2 : "",
        image3 : "",
        image4 : "",
        movieID : reccomended[this.id].id,
      }
    }, 
    async mounted(){
      //Get Overall Data from the API
      const res = await fetch("https://api.themoviedb.org/3/movie/"+this.movieID+"?api_key=b9dfda1d995db256a3b3ae948d044866");
      const movieInfo = await res.json();
      this.title = movieInfo.title;
      this.date = movieInfo.release_date;
      this.language = movieInfo.original_language.toUpperCase();
      this.runtime = movieInfo.runtime;
      this.company = movieInfo.production_companies[0].name;
      for(let i = 0; i < movieInfo.genres.length; i++){
          if(i != movieInfo.genres.length-1){
              this.genre += movieInfo.genres[i].name +", ";
          }
          else{
              this.genre += movieInfo.genres[i].name;
          }
      }
      this.description = movieInfo.overview;
      this.score = movieInfo.vote_average;
      this.poster = "https://image.tmdb.org/t/p/original/"+movieInfo.poster_path;

      const res2 = await fetch("https://api.themoviedb.org/3/movie/"+this.movieID+"/credits?api_key=b9dfda1d995db256a3b3ae948d044866");
      const castCrew = await res2.json();
      let directors = castCrew.crew.filter(crew => crew.job == "Director");
      let writers = castCrew.crew.filter(crew => crew.job == "Screenplay");
      for(let i = 0; i < directors.length; i++){
          if(i != directors.length-1){
              this.director += directors[i].name +", ";
          }
          else{
              this.director += directors[i].name;
          }
      }
      for(let i = 0; i < writers.length; i++){
          if(i != writers.length-1){
              this.writer += writers[i].name +", ";
          }
          else{
              this.writer += writers[i].name;
          }
      }
      for(let i = 0; i < 4; i++){
          if(i != 3){
              this.star += castCrew.cast[i].name +", ";
          }
          else{
              this.star += castCrew.cast[i].name;
          }
      }
      
      const res3 = await fetch("https://api.themoviedb.org/3/movie/"+this.movieID+"/images?api_key=b9dfda1d995db256a3b3ae948d044866");
      const images = await res3.json();
      this.image1 = "https://image.tmdb.org/t/p/original/"+images.backdrops[reccomended[this.id].pictures[0]].file_path;
      this.image2 = "https://image.tmdb.org/t/p/original/"+images.backdrops[reccomended[this.id].pictures[1]].file_path;
      this.image3 = "https://image.tmdb.org/t/p/original/"+images.backdrops[reccomended[this.id].pictures[2]].file_path;
      this.image4 = "https://image.tmdb.org/t/p/original/"+images.backdrops[reccomended[this.id].pictures[3]].file_path;
    },
    methods: {
      round(value){
        return Math.round(value *10) /10;
      },
      moreInfo(){
        console.log(this.movieID);
        this.$emit("selected", this.movieID);
      }
    }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
  #recposter{
      margin-top: 20px;
      margin-left: 20px;
      margin-bottom: 20px;
      width: 300px;
      height: 450px;
  }

  .recTextLeft{
    padding-left: 30px;
    margin: 1rem;
  }

  .recTextRight{
    margin: 1rem;
  }

  #title{
    font-size: 50px;
  }

  #score{
    font-size: 25px;
  }

  #photo{
    margin-top: 20px;
    margin-right: 20px;
    margin-bottom: 10px;
    height: 200px;
    width: 240px;
  }

  #title:hover{
    color: lightblue;
  }

  #ratebars{
    margin-left: -40px;
  }

  #ratebars2{
    margin-left: -50px;
  }

  #recposter:hover{
    border: 1px solid white;
  }

  #rec2photos{
    width: 550px;
  }
</style>
