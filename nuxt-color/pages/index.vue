<template>
  <div>
    <Header/>
    <NuxtLink to="/templates">Templates</NuxtLink>
    <RandomPalette />
  </div>
</template>

<script>
import RandomPalette from '../components/home/RandomPalette.vue';
  export default {
    name: "IndexPage",
    components: { RandomPalette },
    data() {
      return {
        palette: []
      }
    },
    async fetch() {
      const headers = {
        'Content-Type': 'text/plain'
      };
      await this.$axios.$post('http://colormind.io/api/', {
        model: 'default'
      },{headers})
      .then(palette => palette.slice(0, 20))
    },
    fetchOnServer: false,
    // // multiple components can return the same `fetchKey` and Nuxt will track them both separately
    // fetchKey: 'site-sidebar',
}
</script>
