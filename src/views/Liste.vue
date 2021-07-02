<template>
    <div class="home">
        <HelloWorld msg="Welcome"/>
        <br><br>

        <h1 style="font-weight: bold; text-align: center; color: #Ob488c;">Ma liste</h1>
        <br><br>

        <div style="text-align: center;">
            <div v-for="films in mesFilms" :key="films.name">
                <h4 style="color: #e4672c;">Titre du film : {{films.original_title}}</h4>
                <br><h4></h4><img alt="Vue logo" :src="'https://image.tmdb.org/t/p/original/' + films.backdrop_path" height="200">
                <br><h4>Aperçu du film : </h4><p style="margin-left: 5vw; margin-right: 5vw;">{{films.overview}}</p>
                <br><h4>Popularité : {{films.popularity}}</h4>
                <br><h4>Date de sortie : {{films.release_date}}</h4>
                <br>
                <h4>------------------------------------------------------------------------</h4>
                <br>
            
            </div> 
        </div>
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
    }
    },
    mounted(){
        this.getFilms();
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
        }
    }

    }
</script>
