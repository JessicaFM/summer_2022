<template>
  <div>
    <Header/>
    <HomeHeader />
    <HomeCustom />
  </div>
</template>

<script>
import HomeHeader from '../components/home/HomeHeader.vue'
import HomeCustom from '../components/home/HomeCustom.vue'

export default {
  name: "IndexPage",
  components: { HomeHeader, HomeCustom },
}
</script>
