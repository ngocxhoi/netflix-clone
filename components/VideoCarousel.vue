<template>
  <div class="min-w-[1200px] relative">
    <div class="flex flex-col justify-between mr-6">
      <div
        class="flex mb-2 items-center font-semibold text-white text-2xl cursor-pointer"
      >
        {{ category }}
      </div>

      <Carousel
        ref="carousel"
        v-model="currentSlide"
        :items-to-show="8"
        :items-to-scroll="1"
        :wrap-around="true"
        :transition="500"
        snap-align="start"
        class="bg-transparent"
      >
        <Slide
          v-for="(slide, index) in movies"
          :key="slide"
          class="flex items-center object-cover text-white bg-transparent"
        >
          <div
            @click="fullScreenVideo(index)"
            class="object-cover border-4 h-full hover:brightness-125 cursor-pointer"
            :class="
              currentSlide !== index
                ? 'border-transparent'
                : ['border-white', currentSlideObject(slide, index)]
            "
          >
            <img
              :src="'/images/' + slide.name + '.png'"
              style="user-select: none"
              alt=""
              class="pointer-events-none h-full z-[-1]"
            />
          </div>
        </Slide>
        <template #addons>
          <Navigation />
        </template>
      </Carousel>
    </div>
  </div>
</template>

<script setup>
const useMovie = useMovieStore();
let { movie, showFullVideo } = storeToRefs(useMovie);

let currentSlide = ref(0);

const props = defineProps({
  category: String,
  movies: Array,
});

const { movies, category } = toRefs(props);

const currentSlideObject = (slide, index) => {
  if (index === currentSlide.value) {
    movie.value = slide;
  }
};

const fullScreenVideo = (index) => {
  currentSlide.value = index;
  setTimeout(() => (showFullVideo.value = true), 500);
};
</script>

<style>
.carousel__prev,
.carousel__next {
  transform: scale(2) translateY(-25%);
  transition: color 0.25s ease;
}

.carousel__next:hover,
.carousel__prev:hover {
  color: white;
}
</style>
