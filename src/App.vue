<template>
  <v-app>
    <v-main>
      <v-img src="https://picsum.photos/1920/1080?random" cover height="100vh">
        <router-view></router-view>
      </v-img>
    </v-main>
  </v-app>
</template>

<script setup>
import { RouterView } from "vue-router"; //
</script>
