<template>
  <div>
    <section>
      <h1 class="text-5xl font-extrabold dark:text-white">Featured Movies</h1>
      <ul class="grid grid-cols-5 gap">
        <li v-for="mov in movies" :key="mov.id">
          <MovieCard
            :poster_path="mov.poster_path"
            :title="mov.title"
            :id="mov.id"
            :overview="mov.overview"
            :release_date="mov.release_date"
            :popularity="mov.popularity"
            :item="mov"
          />
        </li>
      </ul>
    </section>
    <section>
      <h1 class="text-5xl font-extrabold dark:text-white">
        Featured Tv Series
      </h1>
      <ul class="grid grid-cols-5 gap">
        <li v-for="ser in series" :key="ser.id">
          <SeriesCard
            :poster_path="ser.poster_path"
            :name="ser.name"
            :overview="ser.overview"
            :first_air_date="ser.first_air_date"
            :popularity="ser.popularity"
            :item="ser"
          />
        </li>
      </ul>
    </section>
  </div>
</template>

<script setup>
const movies = useState(() => []);
const series = useState(() => []);

await useFetch('/api/movies/discover', {
  transform: (data) => {
    movies.value = data.movies.results;
    series.value = data.series.results;
  },
});
</script>
