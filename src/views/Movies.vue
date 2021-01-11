<template>
    <v-container>
        <v-layout md12>
            <v-text-field
            v-model="search"
            append-icon="mdi-search"
            placeholder="Buscar"
            single-line
            />
        </v-layout>
        <Loader :isLoading="isLoading" />
        <v-layout wrap md12>
            <v-flex
            v-for="(movie,index) in moviesFilter"
            :key="index"
            :search="search"
            @click="openMovie(movie.id)"
            md3
            sm4
            xs12
            px-2>
                <MovieCard :movie="movie" />
            </v-flex>
        </v-layout>
        <v-btn
        elevation="11"
        large
        medium
        x-large
        @click="masPeliculas()"
        >Siguiente</v-btn>
    </v-container>
</template>

<script>
import ApiService from "@/services/api.service";
import Movie from "@/models/Movie.js";
export default {
    data: function(){
        return {
            movies: [],
            search: "",
            isLoading: true,
            count: 1
        };
    },
    created(){
        setTimeout(() =>{
            this.getMovies();
        },20);
    },
    computed: {
        moviesFilter(){
            return this.movies.filter((e) =>{
                return e.title.toLowerCase().indexOf(this.search.toLowerCase()) !== -1;
            });
        },
    },
    methods:{
        getMovies(){
            ApiService
            .getPopular(1)
            .then((response) =>{
                this.isLoading = false;
                console.log(response.data);
                this.movies = response.data.results.map(movie => new Movie(movie));
                console.log(this.movies);
            })

            .catch(function (error){
                console.log(error);
            });
        },
        openMovie(id){
            this.$router.push({ title: 'Movie', params: {id} })
        },
        masPeliculas(){
            console.log("hola")
        }
    },
};
</script>

<style>

</style>