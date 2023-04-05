<script lang="ts" setup>
import { defineComponent, ref, onMounted } from 'vue';
import axios from 'axios';
import SearchShow from '@/components/SearchShow.vue';
import ShowList from '@/components/ShowList.vue';
import { useQuery } from "@tanstack/vue-query";

interface Movie {
  id: number;
  title: string;
  poster_path: string;
  // Add any other properties you need here
}

const movies = ref<Movie[]>([]);


//const isLoading = ref<Boolean>(false)


const fetchMovies = async () => {
  const response = await axios.get("https://api.themoviedb.org/3/movie/popular", {
    params: {
      api_key: "2336fd5abbe0631a002690648318efa4"
    }
  });
  return response.data.results
};

const { isLoading, isFetching, isError, data, refetch } = useQuery({
  queryKey: ['movies'],
  queryFn: fetchMovies,
})
movies.value = data.value;


onMounted(async () => {
  //await refetch();
  movies.value = data.value;
  console.log("data = ")
  console.log(data.value);
  //movies.value = await fetchMovies()
  //console.log(movies.value)
  /*
  state.topRatedShows = allShows.filter((item) => item.rating?.average >= 7.5)
  GENRES_TO_SHOW.forEach((genre) => {
    state.showsByGenre.push({
      title: `${genre} shows`,
      items: allShows.filter((item) => item.genres?.includes(genre))
    })
  })
  */
  //isLoading.value = false
})
</script>

<template>
  <SearchShow></SearchShow>
  <main>
    <span v-if="isLoading">Loading...</span>
    <ul v-else-if="data">
      <ShowList :items="data">
        <h2>Top Rated Shows</h2>
      </ShowList>
    </ul>
  </main>
  <div>
    <ul>
      <li v-for="movie in movies" :key="movie.id">
        {{ movie.title }}
      </li>
    </ul>
  </div>
</template>
