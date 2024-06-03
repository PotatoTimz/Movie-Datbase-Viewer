<template>
  <!--Header Navigation Bar-->
  <header>
    <nav class="navbar is-dark">
      <div class="navbar-brand">
        <a class="navbar-item">
          <img
            class="logo"
            src="home.png"
            alt="site logo"
            height="50"
            width="50"
            @click="pageMode = 'Home'"
          />
        </a>
      </div>

      <div class="navbar-menu is-dark" id="nav-links">
        <div class="navbar-start">
          <a class="navbar-item" @click="pageMode = 'ProfilePage'">My Profile</a>
          <a class="navbar-item" @click="pageMode = 'NowPlaying'">Now Playing</a>
          <a class="navbar-item" @click="pageMode = 'PopularPage'">Popular Movies Page</a>
          <a class="navbar-item" @click="pageMode = 'SortPage'">Highest Rated Movies</a>
          <a class="navbar-item" @click="pageMode = 'Genres'">Discover by Genres</a>
          <a class="navbar-item" @click="pageMode = 'Review'">Reviews</a>
          <a class="navbar-item" @click="pageMode = 'Search'">Search</a>
        </div>
      </div>
    </nav>
  </header>

  <div v-if="pageMode == `Home`">
    <section class="hero is-info">
      <div class="hero-body">
        <p class="title">MovieRec.com</p>
        <p class="subtitle">What movie are you going to watch next?</p>
      </div>
    </section>
    <ReccomendedPage
      v-bind:id="rec1"
      v-bind:left="true"
      v-on:selected="toMoviePage"
    />
    <ReccomendedPage
      v-bind:id="rec2"
      v-bind:left="false"
      v-on:selected="toMoviePage"
    />
    <ReccomendedPage
      v-bind:id="rec3"
      v-bind:left="true"
      v-on:selected="toMoviePage"
    />
    <ReccomendedPage
      v-bind:id="rec4"
      v-bind:left="false"
      v-on:selected="toMoviePage"
    />
    <ReccomendedPage
      v-bind:id="rec5"
      v-bind:left="true"
      v-on:selected="toMoviePage"
    />
  </div>
  <div v-if="pageMode == `MoviePage`">
    <MoviePage v-bind:id="id" v-on:selected="toRatingsPage" />
  </div>
  <div v-if="pageMode == `RatingPage`">
    <RatingPage v-bind:id="id" />
  </div>
  <div v-if="pageMode == `PopularPage`">
    <PopularPage v-on:selected="toMoviePage" />
  </div>
  <div v-if="pageMode == `Review`">
    <Review v-bind:id="id" />
  </div>
  <div v-if="pageMode == `Search`">
    <Search v-on:selected="toMoviePage" />
  </div>
  <div v-if="pageMode == `SortPage`">
    <SortPage v-bind:id="id" v-on:selected="toMoviePage" />
  </div>
  <div v-if="pageMode == `NowPlaying`">
    <InTheatres v-on:selected="toMoviePage" />
  </div>
  <div v-if="pageMode == `ProfilePage`">
    <ProfilePage v-bind:id="id" v-on:selected="toMoviePage" />
  </div>
  <div v-if="pageMode == `Genres`">x
    <Genre v-on:selected="toMoviePage" />
  </div>
</template>

<script>
import ReccomendedPage from "./components/ReccomendedPage.vue";
import MoviePage from "./components/MoviePage.vue";
import RatingPage from "./components/RatingsPage.vue";
import PopularPage from "./components/PopularPage.vue";
import Review from "./components/Review.vue";
import Search from "./components/Search.vue";
import SortPage from "./components/SortPage.vue";
import InTheatres from "./components/NowPlaying.vue";
import ProfilePage from './components/ProfilePage.vue'
import Genre from "./components/Genre.vue";

let generatedNumbers = [];

while (generatedNumbers.length < 5) {
  let randNum = Math.floor(Math.random() * (9 + 1));
  if (!generatedNumbers.includes(randNum)) {
    generatedNumbers.push(randNum);
  }
}

export default {
  name: "App",
  components: {
    ReccomendedPage,
    MoviePage,
    RatingPage,
    PopularPage,
    Review,
    Search,
    InTheatres,
    ProfilePage,
    Genre,
    SortPage,
  },
  data() {
    return {
      rec1: generatedNumbers[0],
      rec2: generatedNumbers[1],
      rec3: generatedNumbers[2],
      rec4: generatedNumbers[3],
      rec5: generatedNumbers[4],
      id: "1892",
      pageMode: "Home",
    };
  },
  methods: {
    toMoviePage(movieID) {
      console.log("test");

      this.id = movieID;
      this.pageMode = "MoviePage";
    },
    toRatingsPage(personID) {
      this.id = personID;
      console.log("below is the person ID");
      console.log(personID);
      this.pageMode = "RatingPage";
    },
  },
};
</script>

<style></style>
