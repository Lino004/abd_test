<template>
  <v-app-bar
    app
    dark
  >
    <!-- <v-app-bar-nav-icon @click.stop="click()" /> -->
    <v-toolbar-title>
      <img src="@/assets/image.png" height="20px" alt="">
    </v-toolbar-title>
  </v-app-bar>
</template>

<script>
export default {
  methods: {
    click() {
      this.$parent.$parent.drawer = !this.$parent.$parent.drawer
    }
  }
}
</script>

<style>

</style>