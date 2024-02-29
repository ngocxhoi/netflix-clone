<template>
  <div class="fixed w-full h-screen bg-black">
    <div
      v-if="!showFullVideo"
      id="SideNav"
      class="flex z-40 items-center w-[120px] h-screen bg-black relative"
    >
      <img
        src="/images/netflix-logo.png"
        alt=""
        class="absolute top-0 w-[35px] mt-10 ml-10"
      />
      <div>
        <div class="py-2 mx-10 my-6">
          <UIcon
            name="i-heroicons-magnifying-glass"
            class="bg-white h-6 w-6 cursor-pointer"
          />
        </div>
        <div class="py-2 mx-10 my-6 border-b-4 border-b-red-500">
          <UIcon
            name="i-heroicons-home"
            class="bg-white h-6 w-6 cursor-pointer"
          />
        </div>
        <div class="py-2 mx-10 my-6">
          <UIcon
            name="i-heroicons-arrow-trending-up"
            class="bg-white h-6 w-6 cursor-pointer"
          />
        </div>
        <div class="py-2 mx-10 my-6">
          <UIcon
            name="i-heroicons-tv"
            class="bg-white h-6 w-6 cursor-pointer"
          />
        </div>
        <div class="py-2 mx-10 my-6">
          <UIcon
            name="i-heroicons-film"
            class="bg-white h-6 w-6 cursor-pointer"
          />
        </div>
        <div class="py-2 mx-10 my-6">
          <UIcon
            name="i-heroicons-plus"
            class="bg-white h-6 w-6 cursor-pointer"
          />
        </div>
      </div>
    </div>

    <div v-if="!showFullVideo">
      <div
        class="fixed flex z-20 top-0 right-0 w-full h-1/2 bg-black pl-[120px] bg-clip-border"
      >
        <div
          class="absolute z-30 h-[600px] left-[120px] w-[77%] ring-0 top-0 bg-gradient-to-r from-black/80 via-black"
        />
        <MovieDetails v-if="movie" :movie="movie" />

        <video
          v-if="movie"
          :src="'/videos/' + movie.name + '.mp4'"
          autoplay
          loop
          class="absolute z-0 h-[600px] -right-24 top-0"
        />
      </div>

      <!-- MOvie Carousel -->
      <div
        id="MovieCarousel"
        class="fixed z-30 bottom-0 right-0 w-full h-[55%] pl-[120px] overflow-y-auto"
      >
        <VideoCarousel
          class="pb-14 pt-14"
          category="Popular Movies"
          :movies="movies[0]"
        />
        <VideoCarousel
          class="pb-14"
          category="Horror Movies"
          :movies="movies[1]"
        />
        <VideoCarousel
          class="pb-32"
          category="Featured Movies"
          :movies="movies[2]"
        />
      </div>
    </div>
    <div
      v-if="!showFullVideo"
      class="absolute z-20 h-full left-[120px] w-full right-0 top-0 bg-gradient-to-t from-black via-black/70 via-30%"
    />

    <div v-if="showFullVideo">
      <div
        @click="showFullVideo = false"
        class="absolute z-50 p-2 m-4 bg-white/50 rounded-full cursor-pointer"
      >
        <UIcon name="i-heroicons-chevron-left" class="h-6 w-6 bg-white" />
      </div>
      <video
        v-if="movie"
        :src="'/videos/' + movie.name + '.mp4'"
        autoplay
        loop
        controls
        class="absolute z-0 w-screen object-fit -right-24 top-0"
      />
    </div>
  </div>
</template>

<script setup>
import { storeToRefs } from "pinia";
import movies from "~/content/movie.json";

const useMovie = useMovieStore();
let { movie, showFullVideo } = storeToRefs(useMovie);

onMounted(() => {
  setTimeout(() => (movie.value = movies[0][0]), 200);
});
</script>

<style scoped>
#MovieCarousel::-webkit-scrollbar {
  width: 0;
}
</style>
