<template>
  <div>
    <section
      class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4"
    >
      <h1 class="text-5xl font-extrabold dark:text-white">Top Rated Movies</h1>
      <ul
        class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 mx-auto my-8"
      >
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
    <section
      class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4"
    >
      <h1 class="text-5xl font-extrabold dark:text-white">Top Rated Series</h1>
      <ul
        class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 mx-auto my-8"
      >
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

await useFetch('/api/movies/toprated', {
  transform: (data) => {
    movies.value = data.topRatedMovies.results;
    series.value = data.topRatedSeries.results;
  },
});
</script>
