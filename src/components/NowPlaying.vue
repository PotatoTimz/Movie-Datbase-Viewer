<template>
    <div id="UpcomingMovie">
        <div id="underline">
            <strong id="UpcomingTitle">In Cinemas Now</strong>
            <div>Loading movies from {{ startingDate }} - {{ endingDate }}</div>
        </div>

        <section id="MovieInfoUpcoming">
            <div class="columns">

                <div class="column is-half">
                    <div v-for="(movie, index) in upcomingMovies" v-bind:key="index"  id="UpcomingDivider">
                        <div id="TitleCutOff">
                            <strong class="movieTitle is-clickable" v-on:click="moreInfo(movie.id)">{{ movie.title }}</strong>
                            <p>{{ movie.releaseDate }} | {{ movie.language }}</p>
                        </div>
                        <div class="columns" id="MovieDisplay">

                            <div class="column is-5" id="testBorder">
                                <img id="upcomingPoster" class="is-clickable" v-on:click="moreInfo(movie.id)" v-bind:src="movie.poster">
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
                    <div v-for="(movie, index) in upcomingMovies2" v-bind:key="index"  id="UpcomingDivider">
                        
                        <div id="TitleCutOff">
                            <strong class="movieTitle is-clickable"  v-on:click="moreInfo(movie.id)">{{ movie.title }}</strong>
                            <p>{{ movie.releaseDate }} | {{ movie.language }}</p>
                        </div>

                        <div class="columns" id="MovieDisplay">

                            <div class="column is-5">
                                <img id="upcomingPoster" class="is-clickable" v-on:click="moreInfo(movie.id)" v-bind:src="movie.poster">
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
    </div>


     
</template>

<script>
    export default {
        name: "NowPlaying",
        data(){
            return{
                startingDate: 0,
                endingDate: 0,
                upcomingMovies: [],
                upcomingMovies2: [],
                genreList: []
            }
        },
        async mounted(){
            const res2 = await fetch("https://api.themoviedb.org/3/genre/movie/list?api_key=b9dfda1d995db256a3b3ae948d044866&language=en-US");
            const genreInfo = await res2.json();
            this.genreList = genreInfo;

            const res = await fetch("https://api.themoviedb.org/3/movie/now_playing?api_key=b9dfda1d995db256a3b3ae948d044866&language=en-US&page=1");
            const upcomingInfo = await res.json();
            this.startingDate = upcomingInfo.dates.minimum;
            this.endingDate = upcomingInfo.dates.maximum;

            for(let i = 0; i < 5; i++){
                this.upcomingMovies.push({id: upcomingInfo.results[i].id, title: upcomingInfo.results[i].title, language: upcomingInfo.results[i].original_language, description: upcomingInfo.results[i].overview, genre_id: upcomingInfo.results[i].genre_ids, genreList: [], releaseDate: upcomingInfo.results[i].release_date, score: upcomingInfo.results[i].vote_average, popularity: upcomingInfo.results[i].popularity, poster: "https://image.tmdb.org/t/p/original/"+upcomingInfo.results[i].poster_path});

                for(let j = 0; j < this.upcomingMovies[i].genre_id.length; j++){
                    let genreName = this.genreList.genres.filter(genre => (this.upcomingMovies[i].genre_id[j] === genre.id));

                    if(j == this.upcomingMovies[i].genre_id.length-1){
                        this.upcomingMovies[i].genreList += genreName[0].name;
                    }
                    else{
                        this.upcomingMovies[i].genreList += genreName[0].name+", ";
                    }
                }
            }

            for(let i = 5; i < 10; i++){
                this.upcomingMovies2.push({id: upcomingInfo.results[i].id, title: upcomingInfo.results[i].title, language: upcomingInfo.results[i].original_language, description: upcomingInfo.results[i].overview, genre_id: upcomingInfo.results[i].genre_ids, genreList: [], releaseDate: upcomingInfo.results[i].release_date, score: upcomingInfo.results[i].vote_average, popularity: upcomingInfo.results[i].popularity, poster: "https://image.tmdb.org/t/p/original/"+upcomingInfo.results[i].poster_path});
                
                for(let j = 0; j < this.upcomingMovies2[i-5].genre_id.length; j++){
                    let genreName = this.genreList.genres.filter(genre => (this.upcomingMovies2[i-5].genre_id[j] === genre.id));
                    if(j == this.upcomingMovies2[i-5].genre_id.length-1){
                        this.upcomingMovies2[i-5].genreList += genreName[0].name;
                    }
                    else{
                        this.upcomingMovies2[i-5].genreList += genreName[0].name+", ";
                    }
                }
            }
        },
        methods: {
            moreInfo(movieID){
                this.$emit("selected", movieID);
            }
        }
    }
    

</script>

<style>

    #UpcomingTitle{
        font-size: 50px;
    }

    #UpcomingMovie{
        margin: 4rem;
    }

    #underline{
        border-bottom:3px solid black;
    }

    #MovieInfoUpcoming{
        margin-top: 30px;
    }

    .movieTitle{
        font-size:20px;
    }

    .movieTitle:hover{
        color: lightblue;
    }

    #MovieDisplay{
        margin-top: 10px;
    }

    #upcomingPoster{
        width: 275px;
        height: 400px;
    }

    #upcomingPoster:hover{
        border: 4px solid white;
    }

    #TitleCutOff{
        border-bottom:1px solid grey;
        margin-right: 20px;
    }

    #UpcomingDivider{
        height: 525px;
    }
</style>