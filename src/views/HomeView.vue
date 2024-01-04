<template>
  <v-container class="fill-height" fluid>
    <v-row align="center" justify="center">
      <v-col cols="12" sm="8" md="4">
        <v-card class="text-center" color="rgba(255,255,255, 0.85)">
          <template v-slot:title>
            <h2>Welcome!</h2>
          </template>
          <p>Get weather info of any location</p>
          <v-text-field
            v-model="searchTerm"
            append-inner-icon="mdi-magnify"
            clearable
            placeholder="Enter location name here.."
            @click:append-inner="searchCity"
            @keyup.enter="searchCity"
          >
          </v-text-field>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref } from "vue";
import router from "../router/index";
let searchTerm = ref("");
function searchCity() {
  if (searchTerm.value.length > 0)
    router.push(`/city/${searchTerm.value.toLowerCase()}`);
}
</script>
