<template>
<!-- https://vuejs.org/guide/essentials/conditional.html#v-if used for referencing the v-if functions -->
    <section id="PopularPage">
      <section class = "hero is-dark">
      </section>
    </section>
    <section class="hero is-medium is-dark">
    <div class="hero-body">
      <h1 class ="title">Here are some Popular titles Trending right now!</h1>
      <div id ="info">
    <div class="column is-3">
                  <img  class="is-clickable" v-on:click="moreInfo(movieID)" v-bind:src="poster" >
              </div>
   
    <p><strong>Title: </strong>{{ title }}</p>
    <p><br></p>
    <p><strong>Overview: </strong>{{ overview }}</p>
    <p><br></p>
    <p><strong>Release Date: </strong>{{ releaseDate }}</p>
    <p><br></p>
    <!-- <p><strong>Score: </strong>{{ vote}}</p> -->
  
    <div class ="columns">
      <p><strong>Score: </strong></p>
    <div class="field is-horizontal" v-for="i in starz" :key="i">
    <p><img id="stars"  v-bind:src="'star.png'"></p>
  </div>
    </div>
    </div>
  </div>
  </section>
  <!-- show 2 -->
  <section class="hero is-medium is-dark">
    <div class="hero-body">
      <div id ="info">
    <div class="column is-3">
                  <img class="is-clickable" v-on:click="moreInfo(movieID1)" v-bind:src="poster1" >
              </div>
   
    <p><strong>Title: </strong>{{ title1 }}</p>
    <p><br></p>
    <p><strong>Overview: </strong>{{ overview1 }}</p>
    <p><br></p>
    <p><strong>Release Date: </strong>{{ releaseDate1 }}</p>
    <p><br></p>
    <!-- <p><strong>Score: </strong>{{ vote}}</p> -->
  
    <div class ="columns">
      <p><strong>Score: </strong></p>
    <div class="field is-horizontal" v-for="i in starz1" :key="i">
    <p><img id="stars"  v-bind:src="'star.png'"></p>
  </div>
    </div>
    </div>
  </div>
  </section>
  <!-- show3 -->
  <section class="hero is-medium is-dark">
    <div class="hero-body">
      <div id ="info">
    <div class="column is-3">
                  <img class="is-clickable" v-on:click="moreInfo(movieID2)" v-bind:src="poster2" >
              </div>
   
    <p><strong>Title: </strong>{{ title2 }}</p>
    <p><br></p>
    <p><strong>Overview: </strong>{{ overview2 }}</p>
    <p><br></p>
    <p><strong>Release Date: </strong>{{ releaseDate2 }}</p>
    <p><br></p>
  
    <div class ="columns">
      <p><strong>Score: </strong></p>
    <div class="field is-horizontal" v-for="i in starz2" :key="i">
    <p><img id="stars"  v-bind:src="'star.png'"></p>
  </div>
    </div>
    </div>
  </div>
  </section>
  <!-- show4 -->
  <section class="hero is-medium is-dark">
    <div class="hero-body">
      <div id ="info">
    <div class="column is-3">
                  <img class="is-clickable" v-on:click="moreInfo(movieID3)" v-bind:src="poster3" >
              </div>
   
    <p><strong>Title: </strong>{{ title3 }}</p>
    <p><br></p>
    <p><strong>Overview: </strong>{{ overview3 }}</p>
    <p><br></p>
    <p><strong>Release Date: </strong>{{ releaseDate3 }}</p>
    <p><br></p>
  
    <div class ="columns">
      <p><strong>Score: </strong></p>
    <div class="field is-horizontal" v-for="i in starz3" :key="i">
    <p><img id="stars"  v-bind:src="'star.png'"></p>
  </div>
    </div>
    </div>
  </div>
  </section>
  <!-- show5 -->
  <section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID4)" v-bind:src="poster4" >
            </div>
 
  <p><strong>Title: </strong>{{ title4 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview4 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate4 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz4" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show6 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID5)" v-bind:src="poster5" >
            </div>
 
  <p><strong>Title: </strong>{{ title5 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview5 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate5 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz5" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show 7 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID6)" v-bind:src="poster6" >
            </div>
 
  <p><strong>Title: </strong>{{ title6 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview6 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate6 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz6" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show 8 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID7)" v-bind:src="poster7" >
            </div>
 
  <p><strong>Title: </strong>{{ title7 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview7 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate7 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz7" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show9 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID8)" v-bind:src="poster8" >
            </div>
 
  <p><strong>Title: </strong>{{ title8 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview8 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate8 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz8" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show10 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID9)" v-bind:src="poster9" >
            </div>
 
  <p><strong>Title: </strong>{{ title9 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview9 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate9 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz9" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
  
  <!-- <button class="button is-danger" v-on:click=loadFirstFive() >LoadMore</button> -->
  <section class="hero is-dark">
  <center>
  <button class="button is-danger" @click="loadMore = loadFirstFive()">Load More</button>
  </center>
</section>
 
	<!-- <h1 v-if="loadMore==='load'">Vue is awesome!</h1>
	<h1 v-else>Oh no 😢</h1> -->
  
  <!-- Referenced from https://vuejs.org/guide/essentials/conditional.html#v-else-if -->
  <div v-if="loader === 'A'">
    <center>
  <section class="hero is-dark">
   
  <p><strong>Hit the button to load more results</strong></p>
</section>
</center>
</div>
  <div v-else-if="loader === 'B'">
    <!-- show 11 -->
    <section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID10)" v-bind:src="poster10" >
            </div>
 
  <p><strong>Title: </strong>{{ title10 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview10 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate10 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz10" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show 12 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID11)" v-bind:src="poster11" >
            </div>
 
  <p><strong>Title: </strong>{{ title11 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview11 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate11 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz11" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show 13 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID12)" v-bind:src="poster12" >
            </div>
 
  <p><strong>Title: </strong>{{ title12 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview12 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate12 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz12" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show 14 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID13)" v-bind:src="poster13" >
            </div>
 
  <p><strong>Title: </strong>{{ title13 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview13 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate13 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz13" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show 15 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID14)" v-bind:src="poster14" >
            </div>
 
  <p><strong>Title: </strong>{{ title14 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview14 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate14 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz14" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<section class="hero is-dark">
  <center>
  <button class="button is-danger" @click="loadMore = loadNextFive()">Load More</button>
  </center>
</section>
  <div v-if="loader5 === 'A'">
    <center>
    <section class="hero is-dark">
  <p><strong>Hit the button to load more results</strong></p>
   </section>
    </center>
  </div>
  <div v-else-if="loader5 === 'B'">
    <!-- show 16 -->
    <section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID15)" v-bind:src="poster15" >
            </div>
 
  <p><strong>Title: </strong>{{ title15 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview15 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate15 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz15" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show 17 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID16)" v-bind:src="poster16" >
            </div>
 
  <p><strong>Title: </strong>{{ title16 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview16 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate16 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz16" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show18 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID17)" v-bind:src="poster17" >
            </div>
 
  <p><strong>Title: </strong>{{ title17 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview17 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate17 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz17" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show19 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID18)" v-bind:src="poster18" >
            </div>
 
  <p><strong>Title: </strong>{{ title18 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview18 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate18 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz18" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
<!-- show 20 -->
<section class="hero is-medium is-dark">
  <div class="hero-body">
    <div id ="info">
  <div class="column is-3">
                <img class="is-clickable" v-on:click="moreInfo(movieID19)" v-bind:src="poster19" >
            </div>
 
  <p><strong>Title: </strong>{{ title19 }}</p>
  <p><br></p>
  <p><strong>Overview: </strong>{{ overview19 }}</p>
  <p><br></p>
  <p><strong>Release Date: </strong>{{ releaseDate19 }}</p>
  <p><br></p>

  <div class ="columns">
    <p><strong>Score: </strong></p>
  <div class="field is-horizontal" v-for="i in starz19" :key="i">
  <p><img id="stars"  v-bind:src="'star.png'"></p>
</div>
  </div>
  </div>
</div>
</section>
    
  </div>
  <div v-else>
    <p>Hit the Button to see more!</p>
  </div>

  <!-- end of division for the v-if -->
  </div>
  
  <div v-else>
    <p><strong>Hit the button to load more results</strong></p>
</div>



     
  </template>

  <script>


export default {
  name: "PopularPage",
  data(){
    return{
    loadMore: "",
    loader: "A",
    loader5: "A",
      //position1
    title: "",
    overview: "",
    poster: "",
    releaseDate: "",
    vote: "",
    movieID:"",
    star: "",
    
    //position2
    title1:"",
    overview1:"",
    poster1: "",
    releaseDate1: "",
    vote1: "",
    movieID1:"",
    //position3
    title2:"",
    overview2:"",
    poster2: "",
    releaseDate2: "",
    vote2: "",
    movieID2: "",
    //position4
    title3:"",
    overview3:"",
    poster3: "",
    releaseDate3: "",
    vote3: "",
    movieID3: "",
    //position5
    title4:"",
    overview4:"",
    poster4: "",
    releaseDate4: "",
    vote4: "",
    movieID4: "",
    //position6
    title5:"",
    overview5:"",
    poster5: "",
    releaseDate5: "",
    vote5: "",
    movieID5: "",
    //position7
    title6:"",
    overview6:"",
    poster6: "",
    releaseDate6: "",
    vote6: "",
    movieID6: "",
    //position8
    title7:"",
    overview7:"",
    poster7: "",
    releaseDate7: "",
    vote7: "",
    movieID7: "",
    //position9
    title8:"",
    overview8:"",
    poster8: "",
    releaseDate8: "",
    vote8: "",
    movieID8: "",
    //position10
    title9:"",
    overview9:"",
    poster9: "",
    releaseDate9: "",
    vote9: "",
    movieID9: "",
    //postion11
    title10:"",
    overview10:"",
    poster10: "",
    releaseDate10: "",
    vote10: "",
    movieID10: "",
    //postion12
    title11:"",
    overview11:"",
    poster11: "",
    releaseDate11: "",
    vote11: "",
    movieID11: "",
    //postion13
    title12:"",
    overview12:"",
    poster12: "",
    releaseDate12: "",
    vote12: "",
    movieID12: "",
    //postion14
    title13:"",
    overview13:"",
    poster13: "",
    releaseDate13: "",
    vote13: "",
    movieID13: "",
    //postion15
    title14:"",
    overview14:"",
    poster14: "",
    releaseDate14: "",
    vote14: "",
    movieID14: "",
    //postion16
    title15:"",
    overview15:"",
    poster15: "",
    releaseDate15: "",
    vote15: "",
    movieID15: "",
    //postion17
    title16:"",
    overview16:"",
    poster16: "",
    releaseDate16: "",
    vote16: "",
    movieID16: "",
    //postion18
    title17:"",
    overview17:"",
    poster17: "",
    releaseDate17: "",
    vote17: "",
    movieID17: "",
    //postion19
    title18:"",
    overview18:"",
    poster18: "",
    releaseDate18: "",
    vote18: "",
    movieID18: "",
    //postion20
    title19:"",
    overview19:"",
    poster19: "",
    releaseDate19: "",
    vote19: "",
    movieID19: "",


    }
  },
  async mounted(){
    
    //Has 19 values in fetch
    const res = await fetch("https://api.themoviedb.org/3/trending/all/day?api_key=b9dfda1d995db256a3b3ae948d044866")
    const trendingInfo = await res.json();
    console.log("Below is trending info");
    console.log(trendingInfo.results[0]);
    // for (int i =0; i<10; i++){
    this.title = trendingInfo.results[0].title;
    this.overview = trendingInfo.results[0].overview;
    this.poster = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[0].poster_path;
    this.releaseDate = trendingInfo.results[0].release_date
    this.vote = trendingInfo.results[0].vote_average
    this.movieID = trendingInfo.results[0].id
    this.starz = parseInt(this.vote);
    console.log(this.vote);
    console.log(this.title);
    this.star = "star.jpg"
    

    //trending 2
    this.title1 = trendingInfo.results[1].title;
    this.overview1 = trendingInfo.results[1].overview;
    this.poster1 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[1].poster_path;
    this.releaseDate1 = trendingInfo.results[1].release_date
    this.vote1 = trendingInfo.results[1].vote_average
    this.movieID1 = trendingInfo.results[1].id
    this.starz1= parseInt(this.vote1);



    //trending3 
    this.title2 = trendingInfo.results[2].title;
    this.overview2 = trendingInfo.results[2].overview;
    this.poster2 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[2].poster_path;
    this.releaseDate2 = trendingInfo.results[2].release_date
    this.vote2 = trendingInfo.results[2].vote_average
    this.movieID2 = trendingInfo.results[2].id
    this.starz2= parseInt(this.vote2);


     //trending4 
    this.title3 = trendingInfo.results[3].title;
    this.overview3 = trendingInfo.results[3].overview;
    this.poster3 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[3].poster_path;
    this.releaseDate3 = trendingInfo.results[3].release_date
    this.vote3 = trendingInfo.results[3].vote_average
    this.movieID3 = trendingInfo.results[3].id
    this.starz3= parseInt(this.vote3);


    //trending5
    this.title4 = trendingInfo.results[4].title;
    this.overview4 = trendingInfo.results[4].overview;
    this.poster4 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[4].poster_path;
    this.releaseDate4 = trendingInfo.results[4].release_date
    this.vote4 = trendingInfo.results[4].vote_average
    this.movieID4 = trendingInfo.results[4].id
    this.starz4= parseInt(this.vote4);


    //trending6
    this.title5 = trendingInfo.results[5].title;
    this.overview5 = trendingInfo.results[5].overview;
    this.poster5 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[5].poster_path;
    this.releaseDate5 = trendingInfo.results[5].release_date
    this.vote5 = trendingInfo.results[5].vote_average
    this.movieID5 = trendingInfo.results[5].id
    this.starz5= parseInt(this.vote5);


    //trending7
    this.title6 = trendingInfo.results[6].title;
    this.overview6 = trendingInfo.results[6].overview;
    this.poster6 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[6].poster_path;
    this.releaseDate6 = trendingInfo.results[6].release_date
    this.vote6 = trendingInfo.results[6].vote_average
    this.movieID6 = trendingInfo.results[6].id
    this.starz6= parseInt(this.vote6);


    //trending8
    this.title7 = trendingInfo.results[7].title;
    this.overview7 = trendingInfo.results[7].overview;
    this.poster7 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[7].poster_path;
    this.releaseDate7 = trendingInfo.results[7].release_date
    this.vote7 = trendingInfo.results[7].vote_average
    this.movieID7 = trendingInfo.results[7].id
    this.starz7= parseInt(this.vote7);


    //trending9
    this.title8 = trendingInfo.results[8].title;
    this.overview8 = trendingInfo.results[8].overview;
    this.poster8 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[8].poster_path;
    this.releaseDate8 = trendingInfo.results[8].release_date
    this.vote8 = trendingInfo.results[8].vote_average
    this.movieID8 = trendingInfo.results[8].id
    this.starz8= parseInt(this.vote8);


    //trending10
    this.title9 = trendingInfo.results[9].title;
    this.overview9 = trendingInfo.results[9].overview;
    this.poster9 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[9].poster_path;
    this.releaseDate9 = trendingInfo.results[9].release_date
    this.vote9 = trendingInfo.results[9].vote_average
    this.movieID9 = trendingInfo.results[9].id
    this.starz9= parseInt(this.vote9);

    //trending11
    this.title10 = trendingInfo.results[10].title;
    this.overview10 = trendingInfo.results[10].overview;
    this.poster10 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[10].poster_path;
    this.releaseDate10 = trendingInfo.results[10].release_date
    this.vote10 = trendingInfo.results[10].vote_average
    this.movieID10 = trendingInfo.results[10].id
    this.starz10= parseInt(this.vote10);
    
    //trending12
    this.title11 = trendingInfo.results[11].title;
    this.overview11 = trendingInfo.results[11].overview;
    this.poster11 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[11].poster_path;
    this.releaseDate11 = trendingInfo.results[11].release_date
    this.vote11 = trendingInfo.results[11].vote_average
    this.movieID11 = trendingInfo.results[11].id
    this.starz11= parseInt(this.vote11);

    //trending13
    this.title12 = trendingInfo.results[12].title;
    this.overview12 = trendingInfo.results[12].overview;
    this.poster12 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[12].poster_path;
    this.releaseDate12 = trendingInfo.results[12].release_date
    this.vote12 = trendingInfo.results[12].vote_average
    this.movieID12 = trendingInfo.results[12].id
    this.starz12= parseInt(this.vote12);

    //trending14
    this.title13 = trendingInfo.results[13].title;
    this.overview13 = trendingInfo.results[13].overview;
    this.poster13 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[13].poster_path;
    this.releaseDate13 = trendingInfo.results[13].release_date
    this.vote13 = trendingInfo.results[13].vote_average
    this.movieID13 = trendingInfo.results[13].id
    this.starz13= parseInt(this.vote13);

    //trending15
    this.title14 = trendingInfo.results[14].title;
    this.overview14 = trendingInfo.results[14].overview;
    this.poster14 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[14].poster_path;
    this.releaseDate14 = trendingInfo.results[14].release_date
    this.vote14 = trendingInfo.results[14].vote_average
    this.movieID14 = trendingInfo.results[14].id
    this.starz14= parseInt(this.vote14);

    //trending16
    this.title15 = trendingInfo.results[15].title;
    this.overview15 = trendingInfo.results[15].overview;
    this.poster15 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[15].poster_path;
    this.releaseDate15 = trendingInfo.results[15].release_date
    this.vote15 = trendingInfo.results[15].vote_average
    this.movieID15 = trendingInfo.results[15].id
    this.starz15= parseInt(this.vote15);

    //trending17
    this.title16 = trendingInfo.results[16].title;
    this.overview16 = trendingInfo.results[16].overview;
    this.poster16 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[16].poster_path;
    this.releaseDate16 = trendingInfo.results[16].release_date
    this.vote16 = trendingInfo.results[16].vote_average
    this.movieID16 = trendingInfo.results[16].id
    this.starz16= parseInt(this.vote16);

    //trending18
    this.title17 = trendingInfo.results[17].title;
    this.overview17 = trendingInfo.results[17].overview;
    this.poster17 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[17].poster_path;
    this.releaseDate17 = trendingInfo.results[17].release_date
    this.vote17 = trendingInfo.results[17].vote_average
    this.movieID17 = trendingInfo.results[17].id
    this.starz17= parseInt(this.vote17);

    //trending19
    this.title18 = trendingInfo.results[18].title;
    this.overview18 = trendingInfo.results[18].overview;
    this.poster18 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[18].poster_path;
    this.releaseDate18 = trendingInfo.results[18].release_date
    this.vote18 = trendingInfo.results[18].vote_average
    this.movieID18 = trendingInfo.results[18].id
    this.starz18= parseInt(this.vote18);

    //trending20
    this.title19 = trendingInfo.results[19].title;
    this.overview19 = trendingInfo.results[19].overview;
    this.poster19 = "https://image.tmdb.org/t/p/original/" + trendingInfo.results[19].poster_path;
    this.releaseDate19 = trendingInfo.results[19].release_date
    this.vote19 = trendingInfo.results[19].vote_average
    this.movieID19 = trendingInfo.results[19].id
    this.starz19= parseInt(this.vote19);










    











  },
  methods:{
   loadFirstFive() {
        this.loadMore = "load";
        this.loader = "B";
       
      },
      loadNextFive() {
        this.loader5 = "B";
       
      },
      moreInfo(movieID){
                console.log(movieID)
                this.$emit("selected", movieID);
            }
    }
  
}

</script>

<style>
 #stars{
  width: 25px;
  height: 25px;
 }
 #columns{
  padding-top: 50px;
 }

</style>