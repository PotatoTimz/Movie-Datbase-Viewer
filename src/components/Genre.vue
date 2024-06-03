<template>
  <section id="UpcomingMovie">
    <section>
      <div id="underline">
        <strong id="UpcomingTitle">Discover Movies by Genre</strong>
        <div><strong>Currently Searching: </strong> {{ currentGenreName }}</div>
        <div class="field is-horizontal" id="SelectGenre">
          <div class="field-label">
            <label class="label">Genres:</label>
          </div>
          <div class="field-body">
            <div class="field">
              <div class="control">
                <div class="select">
                  <select id="location">
                    <option
                      v-for="(genre, index) in genreList"
                      v-bind:key="index"
                    >
                      {{ genre.name }}
                    </option>
                  </select>
                </div>
              </div>
              <br />
              <button
                id="confirmGenre"
                v-on:click="buttonSelectGenre()"
                class="button is-danger"
              >
                Search
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section v-if="showResults" id="MovieInfoUpcoming">
      <div class="columns">
        <div class="column is-half">
          <div
            v-for="(movie, index) in foundMovies"
            v-bind:key="index"
            id="UpcomingDivider"
          >
            <div id="TitleCutOff">
              <strong class="movieTitle is-clickable" v-on:click="moreInfo(movie.id)">{{
                movie.title
              }}</strong>
              <p>{{ movie.releaseDate }}&emsp;|&emsp;{{ movie.language }}</p>
            </div>
            <div class="columns" id="MovieDisplay">
              <div class="column is-5" id="testBorder">
                <img
                  id="upcomingPoster"
                  class="is-clickable"
                  v-on:click="moreInfo(movie.id)"
                  v-bind:src="movie.poster"
                />
              </div>

              <div class="column is-half">
                <div><strong>Description: </strong>{{ movie.description }}</div>
                <div><strong>Genres: </strong> {{ movie.genreList }}</div>
                <div><strong>Score: </strong>{{ movie.score }}</div>
                <div><strong>Trend Rating: </strong>{{ movie.popularity }}</div>
              </div>
            </div>
          </div>
        </div>

        <div class="column is-half">
          <div
            v-for="(movie, index) in foundMovies2"
            v-bind:key="index"
            id="UpcomingDivider"
          >
            <div id="TitleCutOff">
              <strong class="movieTitle is-clickable" v-on:click="moreInfo(movie.id)">{{
                movie.title
              }}</strong>
              <p>{{ movie.releaseDate }}&emsp;|&emsp;{{ movie.language }}</p>
            </div>

            <div class="columns" id="MovieDisplay">
              <div class="column is-5">
                <img
                  id="upcomingPoster"
                  class="is-clickable"
                  v-on:click="moreInfo(movie.id)"
                  v-bind:src="movie.poster"
                />
              </div>

              <div class="column is-half">
                <div><strong>Description: </strong>{{ movie.description }}</div>
                <div><strong>Genres: </strong> {{ movie.genreList }}</div>
                <div><strong>Score: </strong>{{ movie.score }}</div>
                <div><strong>Trend Rating: </strong>{{ movie.popularity }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <table id="page-selector" class="table">
        <td v-if="numPages > 0" class="is-clickable is-unselectable" v-on:click="loadPage($event.target.innerHTML)">{{ pages[0] }}</td>
        <td v-if="page > 3" class="is-unselectable">...</td>
        <td v-if="numPages > 1" class="is-clickable is-unselectable" v-on:click="loadPage($event.target.innerHTML)">{{ pages[1] }}</td>
        <td v-if="numPages > 2" class="is-clickable is-unselectable" v-on:click="loadPage($event.target.innerHTML)">{{ pages[2] }}</td>
        <td v-if="numPages > 3" class="is-clickable is-unselectable" v-on:click="loadPage($event.target.innerHTML)">{{ pages[3] }}</td>
        <td v-if="page < numPages-2" class="is-unselectable">...</td>
        <td v-if="numPages > 4" class="is-clickable is-unselectable" v-on:click="loadPage($event.target.innerHTML)">{{ pages[4] }}</td>
    </table> 
  </section>
</template>


<script>
import $ from "jquery";

export default {
  name: "GenresPage",
  data() {
    return {
      genreList: [],
      currentGenreName: "None",
      currentGenreID: 0,
      showResults: false,
      foundMovies: [],
      foundMovies2: [],
      page: '1',
      numPages: 0,
      pages: [1, 2, 3, 4, 5]
    };
  },
  async mounted() {
    const res2 = await fetch(
      "https://api.themoviedb.org/3/genre/movie/list?api_key=b9dfda1d995db256a3b3ae948d044866&language=en-US"
    );
    const genreInfo = await res2.json();
    this.genreList = genreInfo.genres;
  },
  methods: {
    loadPage(newPage) {
        if(newPage === this.page)
            return;

        if(newPage < 4)
            this.pages = [1, 2, 3, 4, this.numPages];
        else if(newPage > this.numPages-3)
            this.pages = [1, this.numPages-3, this.numPages-2, this.numPages-1, this.numPages]
        else
            this.pages = [1, newPage-1, newPage, Number(newPage)+1, this.numPages];

        this.page = newPage;
        this.loadRelatedMovies();
        window.scrollTo(0, 0);
    },

    updateSelectedPage() {
        $('.selected-page').removeClass('selected-page').addClass('is-clickable');

        let cells = $('#page-selector').children();
        for(let i=0; i<cells.length; i++) {
            let cell = $(cells[i]);
            if(parseInt(cell.html()) == this.page) {
                cell.removeClass('is-clickable').addClass('selected-page');
                break;
            }
        }
    },

    buttonSelectGenre() {
      this.currentGenreName = $("#location").val();
      let genreInfo = this.genreList.filter(
        (genre) => genre.name === this.currentGenreName
      );
      this.currentGenreID = genreInfo[0].id;
      this.loadRelatedMovies();
      this.showResults = true;
      this.page = 1;
    },

    moreInfo(movieID) {
      this.$emit("selected", movieID);
    },

    async loadRelatedMovies() {
      fetch("https://api.themoviedb.org/3/discover/movie?" +
            "api_key=b9dfda1d995db256a3b3ae948d044866" +
            `&with_genres=${this.currentGenreID}` +
            `&page=${this.page}`)
        .then ((resp)  => resp.json())
        .then ((data)  => this.displayMovies(data))
        .then (()      => this.updateSelectedPage())
        .catch((error) => console.log(error)
      );
    },

    displayMovies(data) {
      this.foundMovies = [];
      this.foundMovies2 = [];
      this.numPages = Math.min(500, data.total_pages);
      this.pages[4] = this.numPages;

      for (let i = 0; i < 10; i++) {
        this.foundMovies.push({
          id: data.results[i].id,
          title: data.results[i].title,
          language: data.results[i].original_language,
          description: data.results[i].overview,
          genre_id: data.results[i].genre_ids,
          genreList: [],
          releaseDate: data.results[i].release_date,
          score: data.results[i].vote_average,
          popularity: data.results[i].popularity,
          poster:
            "https://image.tmdb.org/t/p/original/" +
            data.results[i].poster_path,
        });

        for (let j = 0; j < this.foundMovies[i].genre_id.length; j++) {
          let genreName = this.genreList.filter(
            (genre) => this.foundMovies[i].genre_id[j] === genre.id
          );

          if (j == this.foundMovies[i].genre_id.length - 1) {
            this.foundMovies[i].genreList += genreName[0].name;
          } else {
            this.foundMovies[i].genreList += genreName[0].name + ", ";
          }
        }
      }

      for (let i = 10; i < 20; i++) {
        this.foundMovies2.push({
          id: data.results[i].id,
          title: data.results[i].title,
          language: data.results[i].original_language,
          description: data.results[i].overview,
          genre_id: data.results[i].genre_ids,
          genreList: [],
          releaseDate: data.results[i].release_date,
          score: data.results[i].vote_average,
          popularity: data.results[i].popularity,
          poster:
            "https://image.tmdb.org/t/p/original/" +
            data.results[i].poster_path,
        });

        for (let j = 0; j < this.foundMovies2[i - 10].genre_id.length; j++) {
          let genreName = this.genreList.filter(
            (genre) => this.foundMovies2[i - 10].genre_id[j] === genre.id
          );

          if (j == this.foundMovies2[i - 10].genre_id.length - 1) {
            this.foundMovies2[i - 10].genreList += genreName[0].name;
          } else {
            this.foundMovies2[i - 10].genreList += genreName[0].name + ", ";
          }
        }
      }
    },
  },
};
</script>

<style>
#SelectGenre {
  margin-top: 20px;
  margin-left: -205px;
  margin-bottom: 20px;
}

table tr td {
  padding: 10px;
  border: 2px solid black;
}

td:hover {
  background-color: #f2f2f2;
}

#page-selector {
  margin-left: auto;
  margin-right: auto;
}

.selected-page {
  font-weight: bold;
}
</style>
