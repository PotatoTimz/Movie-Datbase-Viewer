<template>
  <section id="MovieInfo">
    <section class = "hero is-dark">
      <div id="MoviePage" :style='{backgroundImage: `url(${background})`}' >
          <h1 class="is-1 white has-text-white" id="movieTitle">{{ title }}</h1>
          <h2 class = "is-4 has-text-white	" id="movieTagline">{{ subline }}</h2>
          <div class="columns">
              <div class="column is-3">
                  <img id="movieposter" v-bind:src="poster">
              </div>
              <div class="column has-text-white" id="info">
                  <p><strong>Release Date: </strong>{{ date }}</p>
                  <p><strong>Primary Language: </strong>{{ language }}</p>
                  <p><strong>Status: </strong>{{ status }}</p>
                  <p><strong>Production Company: </strong>{{ company }}</p>
                  <p><strong>Budget: </strong>${{ budget }} USD</p>
                  <p><strong>Revenue: </strong>${{ revenue }} USD</p>
                  <p><strong>Genres: </strong>{{ genre }}</p>
                  <br><br>
                  <p>{{ description }}</p>
                  <br><br>

                  <div class="field is-horizontal" id="bars">
                      <div class="field-label">
                          <label><strong>Score</strong></label>
                      </div>
                      <div class="field-body">
                          <div class="field">
                            <svg height="35" width="700">
                              <rect v-bind:width="score/10*700" height="35" fill="green"/>
                              <text y="25" x ="10" fill="white">{{ round(score) }}</text>
                            </svg>
                          </div>
                      </div>
                  </div> 

                  <div class="field is-horizontal " id="bars">
                      <div class="field-label">
                          <label><strong>Trend Score</strong></label>
                      </div>
                      <div class="field-body">
                          <div class="field">
                            <svg height="100" width="700">
                              <rect v-bind:width="trendScore/1000*700" height="35" fill="yellow"/>
                              <text y="25" x ="10" fill="white">{{ round(trendScore) }}</text>
                            </svg>
                          </div>
                      </div>
                  </div> 

              </div>
          </div>
      </div>
    </section>

    <section class = "hero" id="CastandCrew">
      <div class="columns">

        <div class="column is-3">
          <h1 class="title is-1"> Cast</h1>
          <div v-for="(cast, index) in castList" v-bind:key="index">
            <div class="columns">

              <div class="column is-4 devider">
                <img id="actorpicture" class="is-clickable" v-bind:src="cast.picture" v-on:click="personInfo(cast.spot)">
              </div>

              <div class="column is-half">
                <p><strong>Name: </strong> {{ cast.name }}</p>
                <p><strong>Playing: </strong> {{ cast.character }}</p>
              </div>

            <br><br>
            </div>
          </div>
        </div>     

        <div class="column is-3 devider">
          <h1 class="title is-1"> Crew</h1>
          <div v-for="(crew, index) in crewList" v-bind:key="index">
            <div class="columns">

              <div class="column is-4">
                  <img id="actorpicture" class="is-clickable" v-bind:src="crew.picture" v-on:click="personInfoCrew(crew.id)">
              </div>

              <div class="column is-half">
                <p><strong>Name: </strong> {{ crew.name }}</p>
                <p><strong>Job: </strong> {{ crew.job }}</p>
              </div>
              
            <br><br>
            </div>
          </div>
        </div>

        <div class="column devider">
          <h1 class="title is-1"> Reccomendations</h1>
          <div v-for="(reccomendation, index) in reccomandationList" v-bind:key="index">
            <div class="columns">

              <div class="column is-4">
                <img id="MoviePageRecPoster" class="is-clickable" v-bind:src="reccomendation.poster" v-on:click="changeMoviePage(reccomendation.id)">
              </div>

              <div class="column is-half">
                <p id="reccomendationTitle"><strong>{{ reccomendation.name }}</strong></p>
                <p>{{ reccomendation.description }}</p>
                <p><Strong>Score: </Strong>{{ round(reccomendation.score) }}</p>
                <p><Strong>Trend Score: </Strong>{{ round(reccomendation.popularity) }}</p>
              </div>
              
            <br><br>
            </div>
          </div>
        </div>

      </div>
    </section>
  </section>
  <div v-if="pageMode == `RatingPage`">
    <RatingPage/>
  </div>
</template>

<script>
  // import RatingPage from './RatingsPage.vue';
  import $ from 'jquery';
  console.log($("title")[0]);

  export default {
    
    name: 'MoviePage',
    props: {
      id: String
    },
    data() {
      return {
        movieID: this.id,
        title: "", 
        subline: "", 
        background: "", 
        poster: "", 
        date: "", 
        revenue : "", 
        status : "", 
        runtime: "", 
        description : "",
        trendScore: "",
        score : "",
        budget: "", 
        homepage: "",
        company : "", 
        genre : "", 
        language: "", 
        castList: [],
        crewList: [],
        reccomandationList: [],
        pageMode:"Home"
      }
    },
    
    async mounted(){
      //Get Overall Data from the API
      const res = await fetch("https://api.themoviedb.org/3/movie/"+this.movieID+"?api_key=b9dfda1d995db256a3b3ae948d044866");
      const movieInfo = await res.json();
      this.title = movieInfo.title;
      this.subline = movieInfo.tagline,
      this.background = "https://image.tmdb.org/t/p/original/"+movieInfo.backdrop_path;
      this.poster = "https://image.tmdb.org/t/p/original/"+movieInfo.poster_path;
      this.date = movieInfo.release_date;
      this.revenue = movieInfo.revenue;
      this.status = movieInfo.status;
      this.runtime = movieInfo.runtime;
      this.description = movieInfo.overview;
      this.score = movieInfo.vote_average;
      this.budget = movieInfo.budget;
      this.homepage = movieInfo.homepage;
      this.company = movieInfo.production_companies[0].name;
      this.trendScore = movieInfo.popularity;
      this.language = movieInfo.original_language.toUpperCase();
      for(let i = 0; i < movieInfo.genres.length; i++){
          if(i != movieInfo.genres.length-1){
              this.genre += movieInfo.genres[i].name +", ";
          }
          else{
              this.genre += movieInfo.genres[i].name;
          }
      }

      const res2 = await fetch("https://api.themoviedb.org/3/movie/"+this.movieID+"/credits?api_key=b9dfda1d995db256a3b3ae948d044866");
      const castCrew = await res2.json();

      for(let i = 0; i < 10; i++){
        this.castList.push({spot: i,name: castCrew.cast[i].name, character: castCrew.cast[i].character,id: castCrew.cast[i].id ,picture: "https://image.tmdb.org/t/p/original/"+castCrew.cast[i].profile_path});
      }

      // let index = 0;
      //   for(let i = 0; i < 10; i++){
      //     this.crewList.push({spot: index,name: castCrew.crew[index].name, job: castCrew.crew[index].job, id: castCrew.crew[index].id, picture: "https://cdn.pixabay.com/photo/2015/10/05/22/37/blank-profile-picture-973460_1280.png"});
      //     index++;

      //   }
      let previousName = "";
      let index = 0;
    
      while(this.crewList.length != 10){
        if(previousName === castCrew.crew[index].name){
          this.crewList[this.crewList.length-1].job += ", "+castCrew.crew[index].job;
        }
        else{
          if(castCrew.crew[index].profile_path == null){
            this.crewList.push({spot: index,name: castCrew.crew[index].name, job: castCrew.crew[index].job, id: castCrew.crew[index].id, picture: "https://cdn.pixabay.com/photo/2015/10/05/22/37/blank-profile-picture-973460_1280.png"});
          }
          else{
            this.crewList.push({spot: index,name: castCrew.crew[index].name, job: castCrew.crew[index].job, id: castCrew.crew[index].id, picture: "https://image.tmdb.org/t/p/original/"+ castCrew.crew[index].profile_path});
          }
        }
        previousName = castCrew.crew[index].name;
        
        index++;
      }

      const res3 = await fetch("https://api.themoviedb.org/3/movie/"+this.movieID+"/recommendations?api_key=b9dfda1d995db256a3b3ae948d044866&page=1");
      const reccomendations = await res3.json();
      for(let i = 0; i < 4; i++){
        this.reccomandationList.push({name: reccomendations.results[i].original_title, score: reccomendations.results[0].vote_average, poster: "https://image.tmdb.org/t/p/original/"+reccomendations.results[i].poster_path, description : reccomendations.results[i].overview, id: reccomendations.results[i].id, popularity : reccomendations.results[i].popularity});
      }

    },
    methods:{
      async changeMoviePage(id){
        this.movieID = id;

        //Get Overall Data from the API
        const res = await fetch("https://api.themoviedb.org/3/movie/"+this.movieID+"?api_key=b9dfda1d995db256a3b3ae948d044866");
        const movieInfo = await res.json();
        this.title = movieInfo.title;
        this.subline = movieInfo.tagline,
        this.background = "https://image.tmdb.org/t/p/original/"+movieInfo.backdrop_path;
        this.poster = "https://image.tmdb.org/t/p/original/"+movieInfo.poster_path;
        this.date = movieInfo.release_date;
        this.revenue = movieInfo.revenue;
        this.status = movieInfo.status;
        this.runtime = movieInfo.runtime;
        this.description = movieInfo.overview;
        this.score = movieInfo.vote_average;
        this.budget = movieInfo.budget;
        this.homepage = movieInfo.homepage;
        this.trendScore = movieInfo.popularity;
        this.company = movieInfo.production_companies[0].name;
        this.language = movieInfo.original_language.toUpperCase();
        for(let i = 0; i < movieInfo.genres.length; i++){
            if(i != movieInfo.genres.length-1){
                this.genre += movieInfo.genres[i].name +", ";
            }
            else{
                this.genre += movieInfo.genres[i].name;
            }
        }

        const res2 = await fetch("https://api.themoviedb.org/3/movie/"+this.movieID+"/credits?api_key=b9dfda1d995db256a3b3ae948d044866");
        const castCrew = await res2.json();
        this.castList = [];
        this.crewList = [];
      
        for(let i = 0; i < 10; i++){
          // this.castList.push({name: castCrew.cast[i].name, character: castCrew.cast[i].character, picture: "https://image.tmdb.org/t/p/original/"+castCrew.cast[i].profile_path});
          this.castList.push({spot: i,name: castCrew.cast[i].name, character: castCrew.cast[i].character,id: castCrew.cast[i].id ,picture: "https://image.tmdb.org/t/p/original/"+castCrew.cast[i].profile_path});

        }

        let previousName = "";
        let index = 0;
        // for(let i = 0; i < 10; i++){
        //   this.crewList.push({spot: index,name: castCrew.crew[index].name, job: castCrew.crew[index].job, id: castCrew.crew[index].id, picture: "https://cdn.pixabay.com/photo/2015/10/05/22/37/blank-profile-picture-973460_1280.png"});
        //   index++;

        // }
        while(this.crewList.length != 10){
          if(previousName === castCrew.crew[index].name){
            this.crewList[this.crewList.length-1].job += ", "+castCrew.crew[index].job;
          }
          else{
            if(castCrew.crew[index].profile_path == null){
              // this.crewList.push({name: castCrew.crew[index].name, job: castCrew.crew[index].job, picture: "https://cdn.pixabay.com/photo/2015/10/05/22/37/blank-profile-picture-973460_1280.png"});
              this.crewList.push({spot: index,name: castCrew.crew[index].name, job: castCrew.crew[index].job, id: castCrew.crew[index].id, picture: "https://cdn.pixabay.com/photo/2015/10/05/22/37/blank-profile-picture-973460_1280.png"});

            }
            else{
              // this.crewList.push({name: castCrew.crew[index].name, job: castCrew.crew[index].job, picture: "https://image.tmdb.org/t/p/original/"+ castCrew.crew[index].profile_path});
              this.crewList.push({spot: index,name: castCrew.crew[index].name, job: castCrew.crew[index].job, id: castCrew.crew[index].id, picture: "https://cdn.pixabay.com/photo/2015/10/05/22/37/blank-profile-picture-973460_1280.png"});

            }
          }
          previousName = castCrew.crew[index].name;
          index++;
        }
        
        
        const res3 = await fetch("https://api.themoviedb.org/3/movie/"+this.movieID+"/recommendations?api_key=b9dfda1d995db256a3b3ae948d044866&page=1");
        const reccomendations = await res3.json();
        this.reccomandationList = [];

        for(let i = 0; i < 4; i++){
          this.reccomandationList.push({name: reccomendations.results[i].original_title, score: reccomendations.results[0].vote_average, poster: "https://image.tmdb.org/t/p/original/"+reccomendations.results[i].poster_path, backdrop: "https://image.tmdb.org/t/p/original/"+reccomendations.results[i].backdrop_path, description : reccomendations.results[i].overview, id: reccomendations.results[i].id, popularity : reccomendations.results[i].popularity});
        }
      },
      round(value){
        return Math.round(value *10) /10;
      },

      personInfo(i){
       console.log(this.castList);
        console.log("test");
        this.$emit("selected",this.castList[i].id);
      
        
      },
      personInfoCrew(i){
       console.log(i);
        console.log("test");
        this.$emit("selected",i);
      
        
      },
      
     
    },
   
  }
</script>

<style >

#movieTitle, #movieTagline, #movieposter{
  margin-left: 100px;
}

#movieTitle{
  padding-top: 30px;
  font-size: 60px;
  font-weight: 500;
}

#movieTagline{
  font-size: 20px;
  font-style: italic;
  padding-bottom: 10px;
}

#movieposter{
  text-align: center;
  display: block;
  width: 300px;
  height: 500px;
  margin-right: auto;
  padding-bottom: 30px;
}

#info >*{
  margin-right: 20px;
  color: white;
  font-size: 22px;
  margin-left: 50px;
}

#reccomendationTitle{
  font-size: 22px;
}

#CastandCrew{
  padding-left: 150px;
  padding-top: 20px;
}

#actorpicture{
  height: 124px;
  width: 100px;
}

#MovieScale{
  margin-right: 100px;
}

#MoviePage >*{
  text-shadow: -1px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000, 1px 1px 0 #000;
}

#bars{
  margin-left: -10px;
}

#actorpicture:hover{
  border: 1px solid white;
}

#MoviePageRecPoster:hover{
  border: 4px solid white;
}
</style>
