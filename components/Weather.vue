<template>
  <h1 class="text-white text-center mb-8 font-semibold text-3xl">
    Weather App
  </h1>
  <form v-on:submit.prevent="searchCity">
    <label
      for="default-search"
      class="mb-2 text-sm font-medium text-gray-900 sr-only"
      >Search</label
    >
    <div class="flex items-center justify-center">
    <div class="relative ">
      <div
        class="absolute inset-y-0 start-0 flex items-center ps-3 pointer-events-none"
      >
        <svg
          class="w-5 h-5 text-white"
          aria-hidden="true"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 20 20"
        >
          <path
            stroke="currentColor"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"
          />
        </svg>
      </div>
      <input
        type="search"
        id="default-search"
        class="block w-[300px] md:w-[700px] p-4 ps-10 text-xl text-white border border-gray-300 placeholder:text-white rounded-2xl bg-transparent focus:ring-cyan-500 focus:border-cyan-500"
        placeholder="Search for a city"
        required
        v-model="city"
      />
    </div>
  </div>
  </form>

  <div
     class="w-[320px] md:w-[900px] h-[400px] md:h-[350px] p-8 mt-20 box mx-auto rounded-lg bg-transparent border-[4px] shadow-xl shadow-cyan-600 border-cyan-500 dark:bg-gray-900 dark:text-gray-100 hover:cursor-pointer  hover:-translate-y-1 motion-reduce:transition-none motion-reduce:hover:transform-none transition duration-150 easy-in-out"
  >
    <div class="flex justify-between space-x-8">
      <div class="flex flex-col items-center">
        <img
          :src="weatherData.current ? weatherData.current.condition.icon : ''"
          class="w-[90px] h-[90px]"
          alt="Weather icon"
        />
        <h1 class="text-lg md:text-2xl text-center font-semibold text-white">
          {{
            weatherData.location
              ? `${weatherData.location.name}, ${weatherData.location.country}`
              : ""
          }}
        </h1>
      </div>
      <span class="font-bold text-4xl md:text-8xl text-white"
        >{{ weatherData.current ? weatherData.current.temp_c : " " }}°C</span
      >
    </div>
    <div class="flex justify-between mt-20 space-x-4 dark:text-gray-400">
      <div class="flex flex-col items-center justify-center">
        <div>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="icon icon-tabler icon-tabler-wind text-white"
            width="30"
            height="30"
            viewBox="0 0 24 24"
            stroke-width="2"
            stroke="currentColor"
            fill="none"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path stroke="none" d="M0 0h24v24H0z" fill="none" />
            <path d="M5 8h8.5a2.5 2.5 0 1 0 -2.34 -3.24" />
            <path d="M3 12h15.5a2.5 2.5 0 1 1 -2.34 3.24" />
            <path d="M4 16h5.5a2.5 2.5 0 1 1 -2.34 3.24" />
          </svg>
        </div>
        <div class="flex flex-col items-center justify-center">
          <h2 class="text-lg md:text-2xl text-white">
            {{ weatherData.current ? weatherData.current.wind_kph : " " }} km/h
          </h2>
          <h2 class="text-white text-lg md:text-2xl">Wind</h2>
        </div>
      </div>
      <div class="flex flex-col items-center justify-center">
        <div>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="icon icon-tabler icon-tabler-droplet-half-2-filled text-white"
            width="30"
            height="30"
            viewBox="0 0 24 24"
            stroke-width="2"
            stroke="currentColor"
            fill="none"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path stroke="none" d="M0 0h24v24H0z" fill="none" />
            <path
              d="M13.905 2.923l.098 .135l4.92 7.306a7.566 7.566 0 0 1 1.043 3.167l.024 .326c.007 .047 .01 .094 .01 .143l-.002 .06c.056 2.3 -.944 4.582 -2.87 6.14c-2.969 2.402 -7.286 2.402 -10.255 0c-1.904 -1.54 -2.904 -3.787 -2.865 -6.071a1.052 1.052 0 0 1 .013 -.333a7.66 7.66 0 0 1 .913 -3.176l.172 -.302l4.893 -7.26c.185 -.275 .426 -.509 .709 -.686c1.055 -.66 2.446 -.413 3.197 .55zm-2.06 1.107l-.077 .038l-.041 .03l-.037 .036l-.033 .042l-4.863 7.214a5.607 5.607 0 0 0 -.651 1.61h11.723a5.444 5.444 0 0 0 -.49 -1.313l-.141 -.251l-4.891 -7.261a.428 .428 0 0 0 -.5 -.145z"
              stroke-width="0"
              fill="currentColor"
            />
          </svg>
        </div>
        <div class="flex flex-col items-center justify-center">
          <h2 class="text-lg md:text-2xl text-white">
            {{ weatherData.current ? weatherData.current.humidity : " " }}%
          </h2>
          <h2 class="text-white text-lg md:text-2xl">Humidity</h2>
        </div>
      </div>
      <div class="flex flex-col items-center justify-center">
        <div>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="icon icon-tabler icon-tabler-uv-index text-white"
            width="30"
            height="30"
            viewBox="0 0 24 24"
            stroke-width="2"
            stroke="currentColor"
            fill="none"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path stroke="none" d="M0 0h24v24H0z" fill="none" />
            <path
              d="M3 12h1m16 0h1m-15.4 -6.4l.7 .7m12.1 -.7l-.7 .7m-9.7 5.7a4 4 0 1 1 8 0"
            />
            <path d="M12 4v-1" />
            <path d="M13 16l2 5h1l2 -5" />
            <path d="M6 16v3a2 2 0 1 0 4 0v-3" />
          </svg>
        </div>
        <div class="flex flex-col items-center justify-center">
          <h2 class="text-lg md:text-2xl text-white">
            {{ weatherData.current ? weatherData.current.pressure_in : " " }}
          </h2>
          <h2 class="text-white text-lg md:text-2xl">Pressure</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
const config = useRuntimeConfig();

let city = ref("Panamá");
let weatherData = ref({});

const api_base = config.public.api_key;

const searchCity = async () => {
  const url = `https://api.weatherapi.com/v1/current.json?key=${api_base}&q=${city.value}&aqi=no`;

  try {
    const response = await axios.get(url);
    weatherData.value = response.data;
    console.log(weatherData.value);
  } catch (error) {
    console.error(error);
  }
};

onMounted(searchCity);
</script>
