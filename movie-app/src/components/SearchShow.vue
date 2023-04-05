<script lang="ts" setup>
import { ref } from "vue";
import axios from "axios";
import { useQuery } from "@tanstack/vue-query";
import { watch } from "vue";
import ShowList from "./ShowList.vue";
import LoadingSpinner from "./LoadingSpinner.vue";

interface Movie {
  id: number;
  title: string;
  backdrop_path: string;
  // Add any other properties you need here
}

const input = ref("");
const api_key = "2336fd5abbe0631a002690648318efa4"
const items = ref<Movie[]>([])

const fetchMovies = async () => {
    try {
        console.log(input.value)
        const response = await axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${api_key}&language=en-US&query=${input.value}&page=1&include_adult=false`, {
        });
        return response.data.results
    } catch {
        console.log("error")
    }
};

const { isLoading, isFetching, isError, data, refetch } = useQuery({
            queryKey: ['search'],
            queryFn: fetchMovies
        })

watch(input,
    async () => {
        if (input.value) {
            await refetch();
            items.value = data.value
        }
    }
)

</script>

<template>
  <div class="search-shows">
    <label>Search your favorite show 🎥</label>
    <input type="text" placeholder="Search show" v-model="input" />

    <div class="loading" v-show="isLoading">
      <LoadingSpinner />
    </div>

    <ShowList
      v-if="!isLoading && items.length > 0 && input.length > 0"
      class="search-results"
      :items="items"
    >
      <h2>Search results</h2>
    </ShowList>
  </div>
</template>

<style scoped>
.loading {
  display: flex;
  width: 100%;
  justify-content: center;
}

input {
    justify-content: center;
width: 100%
}

.search-shows {
  margin-bottom: calc(var(--spacing) * 3);
    margin-bottom: 50px;
}

.search-results {
  margin-top: calc(var(--spacing) * 2);
}

label {
  display: block;
  font-weight: 700;
  margin-bottom: var(--spacing);
}
</style>