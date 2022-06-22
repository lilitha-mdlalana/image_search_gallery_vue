<template>
  <section>
    <h1 class="text-white text-3xl font-bold text-center pt-3">
      Vue Photo Gallery
    </h1>
    <div class="flex flex-col items-center">
      <input type="text" v-model="value" class="focus:outline-none p-2 m-3" />
      <button>Submit</button>
    </div>
  </section>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      value: "",
    };
  },
};
</script>

<style>
#app {
  @apply bg-slate-500 w-full h-screen;
}
</style>
