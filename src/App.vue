<template>
  <v-app class="app">
    <v-main>
      <v-layout fill-height>
        <router-view />
      </v-layout>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({ }),
};
</script>

<style lang="scss" scoped>
.app {
  font-family: "Montserrat", sans-serif;
}
</style>
