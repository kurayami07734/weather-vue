<template>
  <v-container class="fill-height" fluid>
    <v-row align="center" justify="center">
      <v-col cols="12" sm="8" md="4">
        <v-card
          class="mx-auto px-auto py-2 my-2"
          color="rgba(255,255,255, 0.85)"
        >
          <v-progress-circular
            v-if="isLoading"
            indeterminate
            color="primary"
          ></v-progress-circular>

          <div v-else-if="error">{{ error }}</div>
          <v-card v-else flat color="rgba(255,255,255, 0.85)">
            <template v-slot:title>
              <div>
                <span class="text-h2">{{
                  $route.params.name.toLocaleUpperCase()
                }}</span>
                <section class="text-h4">
                  {{ regionNames.of(weatherData.sys.country) }}
                </section>
                {{
                  new Date(weatherData.dt * 1000).toLocaleDateString("en-IN")
                }}
              </div>
              <div>
                {{ weatherData.weather[0].description }}
              </div>
              <h3 class="text-h1">{{ weatherData.main.temp }} °C</h3>
              <div>
                Feels like
                <section class="text-h3">
                  {{ weatherData.main.feels_like }} °C
                </section>
              </div>
            </template>
          </v-card>
          <v-card-actions>
            <v-btn to="/"> Go Back </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script setup>
import { useRoute } from "vue-router";
const route = useRoute();
import { ref, onMounted } from "vue";
const isLoading = ref(true);
const error = ref("");
const weatherData = ref({});
onMounted(() => fetchWeather());
const regionNames = new Intl.DisplayNames(["en"], { type: "region" });
async function fetchWeather() {
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${
    route.params.name
  }&appid=${import.meta.env.VITE_API_KEY}&units=metric`;
  try {
    const response = await fetch(url);
    if (response.status != 200) {
      error.value = response.statusText;
      weatherData.value = {};
    }
    weatherData.value = await response.json();
    // console.log(weatherData.value);
    isLoading.value = false;
  } catch (e) {
    console.log(e.toString());
    error.value = e.toString();
  }
}
</script>
