<template>
  <section>
    <h1 class="text-white text-3xl font-bold text-center pt-3">
      Vue Photo Gallery
    </h1>
    <form class="flex items-center justify-center" @submit.prevent>
      <input type="text" v-model="value" class="focus:outline-none p-2 m-3" />
      <submit-button text="Submit" @click="getImages(value)" />
    </form>
  </section>
  <section
    id="picture-of-the-day"
    class="flex flex-col items-center h-full"
    v-if="images.length < 1"
  >
    <h1 class="text-white text-3xl">Random Image</h1>
    <img :src="randomImage" class="rounded w-96 h-96" />
  </section>
  <section
    id="images"
    class="md:grid md:grid-cols-3 md:gap-3 flex flex-col m-2"
  >
    <img
      v-for="image in images"
      :key="image.id"
      :src="image.urls.regular"
      class="rounded w-96 h-96"
    />
  </section>
</template>

<script>
import axios from "axios";
import SubmitButton from "@/components/Shared/Button.vue";
export default {
  name: "MainLayout",
  data() {
    return {
      value: "",
      randomImage: "",
      images: [],
    };
  },
  components: {
    SubmitButton,
  },
  methods: {
    async getImages(query) {
      const response = await axios.get(
        `https://api.unsplash.com/search/photos?page=1&query=${query}&client_id=${process.env.VUE_APP_ACCESS_KEY}`
      );
      this.images = response.data.results;
    },
    async getRandomPhotos() {
      const response = await axios.get(
        `${process.env.VUE_APP_BASE_URL}photos/random/?client_id=${process.env.VUE_APP_ACCESS_KEY}`
      );
      this.randomImage = response.data.urls.regular;
    },
  },
  mounted() {
    this.getRandomPhotos();
  },
};
</script>

<style>
#app {
  @apply bg-slate-500 w-full min-h-screen;
}
</style>
