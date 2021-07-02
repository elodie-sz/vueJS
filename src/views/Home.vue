<template>
  <div class="home">
      <input type="search" id="site-search" name="q" placeholder="Rechercher..."
      aria-label="Search through site content" style="text-align: center; margin-left: 35vw;">
      <HelloWorld msg="Welcome"/>
      <br><br>

      <div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
          <div v-for="films in mesFilms" :key="films.name">
            <img alt="Vue logo" :src="'https://image.tmdb.org/t/p/original/' + films.poster_path" height="300">
          
            <hello-world
                :movieImage="path+films.poster_path"
                :getDetails="getDetails"
                :id="films.id"
            >
            </hello-world>
          </div> 
      </div>

      <div>
            <button v-if="pageIndex!=1" @click="getPage(pageIndex-1)">Précédent</button>
            <button @click="getPage(pageIndex+1)">Suivant</button>
      </div>

      <!-- modal -->
      <modal name="details" :height="300">
          <div v-if="oneMovie">
            <div class="detailsContainer">
                <!-- <img alt="Vue logo" :src="'https://image.tmdb.org/t/p/original/' + films.poster_path" height="300"> -->
                <img :src="path+oneMovie.poster_path" width="200">
                <div>
                  <h4>{{oneMovie.original_title}}</h4>
                  <h4>Synopsis : </h4><p>{{oneMovie.overview}}</p>
                  <h4>Note : </h4><p>{{oneMovie.vote_average}}/10</p>
                  <h4>Popularité : {{oneMovie.popularity}}</h4>
                  <h4>Date de sortie : {{oneMovie.release_date}}</h4>
                </div>
            </div>
            <div>
              <button @click="addToList(oneMovie)">+ Ajouter à ma liste</button>
            </div>
          </div>
      </modal>

  </div>


</template>

<script>
  import HelloWorld from '../components/HelloWorld.vue'
  import axios from 'axios';

  export default {
    name: 'Home',

    components: {
      HelloWorld,
    },
    data(){
    return{
      mesFilms : null,
      path : "https://image.tmdb.org/t/p/original",
      oneMovie:null,
      release_data: null,
      pageIndex: null,
      Liste:[]
    }
  },
  mounted(){
    this.getFilms();
    console.log("Ma liste : ", localStorage.getItem('Liste'));
    this.liste = JSON.parse(localStorage.getItem('Liste'));
  },
  methods:{
    getFilms(){
      axios
        .get('https://api.themoviedb.org/3/movie/popular?api_key=029a8e8d1260924d13c45ff97e1bcb8a&language=fr')
        .then((response) =>{
            this.mesFilms = response.data.results
            console.log(this.mesFilms)
        } )
        .catch(error => console.log(error))
    },
    hide() {
      this.$modal.hide('details')
    },

    async getDetails(movieId){
        this.$modal.show('details');
        const films = axios.get(`https://api.themoviedb.org/3/movie/${movieId}?api_key=029a8e8d1260924d13c45ff97e1bcb8a&language=fr`)
        this.oneMovie = films.data;
        const yearRelease = this.oneMovie.release_data.split('-');
        this.release_data = yearRelease[0];
    }, 
    async getPage(index){
      this.pageIndex = index;
      const moviesTemp = await axios.get('https://api.themoviedb.org/3/movie/popular?api_key=029a8e8d1260924d13c45ff97e1bcb8a&language=fr')
      this.mesFilms = moviesTemp.data.results;
    }
    ,
    addToList(films)
    {
      this.Liste.push(films);
      console.log(this.Liste)
      localStorage.setItem('Liste', JSON.stringify(this.Liste));
    }
  }

  }
</script>
