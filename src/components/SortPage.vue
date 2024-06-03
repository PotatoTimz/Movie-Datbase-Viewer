<template>
  <section id="Review">
    <section class="hero is-dark">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">Top 20 Rated Movies</h1>
          <div class="columns is-multiline">
            <div
              v-for="movie in sortedMovies"
              :key="movie.id"
              class="column is-one-fifth"
            >
              <div class="card">
                <div class="card-image" @click="moreInfo(movie.id)">
                  <figure class="image is-2by3">
                    <img
                      :src="getImageUrl(movie.poster_path)"
                      :alt="movie.title"
                    />
                    <div class="rating">{{ movie.vote_average }}</div>
                  </figure>
                </div>
                <div class="card-content">
                  <div class="media-content">
                    <p class="title is-6">{{ movie.title }}</p>
                    <p class="subtitle is-7">{{ movie.release_date }}</p>
                  </div>
                  <div class="content">
                    {{ movie.overview }}
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </section>
</template>
<script>
export default {
  name: "SortPage",
  data() {
    return {
      movies: [],
      apiKey: "b9dfda1d995db256a3b3ae948d044866",
      baseUrl: "https://api.themoviedb.org/3",
    };
  },
  created() {
    this.fetchMovies();
  },
  methods: {
    fetchMovies() {
      fetch(
        `${this.baseUrl}/movie/top_rated?api_key=${this.apiKey}&language=en-US&page=1`
      )
        .then((response) => response.json())
        .then((data) => {
          this.movies = data.results;
          this.sortMovies();
        })
        .catch((error) => console.error(error));
    },
    getImageUrl(posterPath) {
      if (!posterPath) {
        return "https://via.placeholder.com/500x750?text=Poster+not+available";
      }
      return `https://image.tmdb.org/t/p/w500${posterPath}`;
    },
    sortMovies() {
      this.movies.sort((a, b) => b.vote_average - a.vote_average);
    },
    showDetails(id) {
      // make a request to get movie details using the movie id
      fetch(`${this.baseUrl}/movie/${id}?api_key=${this.apiKey}&language=en-US`)
        .then((response) => response.json())
        .then((data) => {
          // display the movie details using an alert or a modal
          alert(
            `Title: ${data.title}\nRelease Date: ${data.release_date}\nOverview: ${data.overview}`
          );
        })
        .catch((error) => console.error(error));
    },
    moreInfo(movieID){
        this.$emit("selected", movieID);
    },
  },
  computed: {
    sortedMovies() {
      return this.movies;
    },
  },
};
</script>

<style scoped>
.rating {
  position: absolute;
  top: 10px;
  left: 10px;
  background-color: #fff;
  color: #000;
  font-size: 1.5rem;
  font-weight: bold;
  padding: 5px 10px;
  border-radius: 5px;
}

.card {
  position: relative;
  overflow: hidden;
  margin-bottom: 1rem;
  box-shadow: 0 2px 3px rgba(10, 10, 10, 0.1);
}

.card-image {
  position: relative;
  display: block;
}

.card-image img {
  display: block;
  width: 100%;
  height: auto;
  transition: transform 0.2s ease-out;
}

.card-image:hover img {
  transform: scale(1.05);
}

.card-content {
  padding: 1rem;
}

.card-content .media-content {
  margin-bottom: 0.5rem;
}

.card-content .title {
  font-size: 1.2rem;
  font-weight: bold;
}

.card-content .subtitle {
  font-size: 1rem;
  color: #666;
}

.card-content .content {
  margin-top: 0.5rem;
  font-size: 0.9rem;
  line-height: 1.4rem;
  overflow: hidden;
  text-overflow: ellipsis;
  max-height: 4.2rem;
}

.card-content .content:hover {
  max-height: none;
}
</style>

