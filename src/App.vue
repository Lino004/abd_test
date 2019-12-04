<template>
  <v-app id="inspire">
    <NavMenu :drawer="drawer"/>

    <NavHeader/>

    <v-content>
      <v-container
        class="fill-height"
        fluid
      >
        <router-view/>
      </v-container>
    </v-content>
    
    <Footer/>

  </v-app>
</template>

<script>
  import NavMenu from '@/components/NavMenu.vue'
  import NavHeader from '@/components/NavHeader.vue'
  import Footer from '@/components/Footer.vue'

  export default {
    components: {
      NavMenu,
      NavHeader,
      Footer,
    },
    data: () => ({
      drawer: false,
    }),
  }
</script>

<style>
@import './css/generale.css';
</style>