<template>
  <section class="hero is-dark">
    <div id="query-entry">
      <h1>Search for a Movie</h1>
      <div class="field">
        <div class="control">
          <input id="query" class="input" type="text" v-model="query" v-on:keyup.enter="submitQuery(true)" placeholder="Movie title">
        </div>
      </div>

      <!-- Optional fields -->
      <p class="is-clickable is-unselectable" v-on:click="toggleOptionalFields">
        Advanced search options {{ optionalFieldArrow }}
      </p>
      <div id="optional-fields" v-if="optionalFields">
        <div class="field is-horizontal">
          <div class="field-label is-normal">
            <label class="label has-text-white">Year:</label>
          </div>
          <div class="field-body">
            <div class="select">
              <select v-model="year">
                <option v-for="year in yearOptions" v-bind:key="year">{{ year }}</option>
              </select>
            </div>
          </div>
        </div>
      </div>

      <!-- Search button -->
      <div class="field">
        <button id="search-button" class="button" v-on:click="submitQuery(true)">Search</button>
      </div>
    </div>
  </section>

  <!-- Search results -->
  <div id="search-results" v-if="results.length > 0">
    <h2>Results ({{ 20*(page-1)+1 }}-{{ Math.min(20*page, numResults) }} of {{ numResults }}):</h2>
    <div class="movie-result columns is-clickable" v-for="movie in results" v-bind:key="movie" v-on:click="moreInfo(movie.id)">
      <img v-bind:src="movie.poster">
      <div id="result-info">
        <p><strong>{{ movie.title }}</strong></p>
        <p>{{ movie.info }}</p>
        <br>
        <p>{{ movie.overview }}</p>
      </div>
    </div>

    <!-- Page selector -->
    <table id="page-selector" class="table">
      <td v-if="numPages > 0" class="is-clickable is-unselectable" v-on:click="loadPage($event.target.innerHTML)">{{ pages[0] }}</td>
      <td v-if="page > 3" class="is-unselectable">...</td>
      <td v-if="numPages > 1" class="is-clickable is-unselectable" v-on:click="loadPage($event.target.innerHTML)">{{ pages[1] }}</td>
      <td v-if="numPages > 2" class="is-clickable is-unselectable" v-on:click="loadPage($event.target.innerHTML)">{{ pages[2] }}</td>
      <td v-if="numPages > 3" class="is-clickable is-unselectable" v-on:click="loadPage($event.target.innerHTML)">{{ pages[3] }}</td>
      <td v-if="page < numPages-2" class="is-unselectable">...</td>
      <td v-if="numPages > 4" class="is-clickable is-unselectable" v-on:click="loadPage($event.target.innerHTML)">{{ pages[4] }}</td>
    </table>
  </div>
</template>




<script>
  import $ from 'jquery';

  export default {
    name: 'SearchPage',
    inheritAttrs: false,

    data() {
      return {
        optionalFields: false,
        optionalFieldArrow: '▾',
        yearOptions: ['Any'],
        pages: [1, 2, 3, 4, 5],
        numPages: 0,
        numResults: 0,
        genres: [],
        results: [],

        // Query parameters
        query: '',
        year: '',
        page: '1'
      }
    },


    async mounted() {

      // Get genre list
      fetch('https://api.themoviedb.org/3/genre/movie/list?' +
            'api_key=b9dfda1d995db256a3b3ae948d044866&language=en-US')
        . then((resp)  => resp.json())
        . then((data)  => this.genres = Object.assign({}, ...(data.genres.map(genre => ({[genre.id]: genre.name})))))
        .catch((error) => console.log(error)
      );

      // Generate year options
      let year = new Date().getFullYear();
      for(; year>1878; year--) {
        this.yearOptions.push(year);
      }
    },


    methods: {
      toggleOptionalFields() {
        this.optionalFields = !this.optionalFields;
        this.optionalFieldArrow = (this.optionalFieldArrow === '▾')?  '▴' : '▾';
      },

      
      async submitQuery(newQuery) {
        if(newQuery) this.page = '1';
        $('#query').blur();           // Remove cursor focus from input

        fetch('https://api.themoviedb.org/3/search/movie?' +
              'api_key=b9dfda1d995db256a3b3ae948d044866' +
              `&query=${this.query}&year=${this.year}&page=${this.page}`)
          .then ((resp)  => resp.json())
          .then ((data)  => this.displayResults(data))
          .then (()      => this.updateSelectedPage())
          .catch((error) => console.log(error)
        );
      },


      displayResults(data) {
        this.numPages   = data.total_pages;
        this.numResults = data.total_results;
        this.pages[4]   = this.numPages;
        this.results    = [];

        for(let result of data.results) {
          let resultData = {
            id:       result.id,
            title:    result.title,
            overview: result.overview,
            info:     ''
          };

          if(result.poster_path !== null)
            resultData.poster = 'https://image.tmdb.org/t/p/original/' + result.poster_path;

          // Year and genre(s)
          if(result.release_date !== undefined)
            resultData.info = result.release_date.slice(0, 4);

          if(result.genre_ids.length > 0) {
            if(resultData.info !== '')
              resultData.info += '\u2003|\u2003';

            resultData.info += this.genres[result.genre_ids[0]];
            for(let i=1; i<result.genre_ids.length; i++)
              resultData.info += ', ' + this.genres[result.genre_ids[i]];
          }

          this.results.push(resultData);
        }
      },


      // Loads a new page of search results
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
        this.submitQuery(false);
        window.scrollTo(0, 0);
      },


      // Updates the selected cell in the page selector table
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


      moreInfo(movieID) {
        this.$emit('selected', movieID);
      }
    }
  }
</script>




<style>
  h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
  }

  h2 {
    font-size: 2rem;
  }

  #query-entry {
    margin: 4rem;
  }

  #optional-fields {
    margin: 1rem;
    width: 1000px;
  }

  #search-button {
    margin-top: 1rem;
  }

  #search-results {
    width: 50%;
    min-width: 50rem;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 2rem;
  }

  .movie-result {
    height: 12rem;
    width: 100%;
    margin: 1rem;
    border: 1px solid black;
    border-radius: 0.5rem;
    overflow: hidden;
  }
  
  .movie-result:hover {
    border: 1px solid rgb(175, 175, 175);
  }

  #result-info {
    margin: 1rem;
    overflow: hidden;
  }

  #result-info strong {
    font-size: 1.5rem;
  }

  #page-selector {
    margin-left: auto;
    margin-right: auto;
  }

  .selected-page {
    font-weight: bold;
  }
</style>
