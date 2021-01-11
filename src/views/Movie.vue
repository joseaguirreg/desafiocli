<template>
  <v-container>
      <h1>Nombre: {{ $movie.original.title }}</h1>
      <Loader :isLoading="isLoading" />
      <CountryCard v-if="!isLoading" :movie="movie" />
  </v-container>
</template>

<script>
import apiService from "@/services/api.service";
export default {
    data(){
        return{
            movie: {},
            isLoading: true,
        };
    },
    created(){
        this.getMovie();
    },
    methods: {
        getMovie(){
            apiService
            .getMovie(this.$route.params.id)
            .then((response) =>{
                this.isLoading = false;
                this.movie = response.data[0];
            })
            .catch((error) => {
                this.isLoading = false;
                alert(error);
            })
        }
    },
}
</script>

<style>

</style>