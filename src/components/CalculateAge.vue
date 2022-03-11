<template>
  <div id="app">
    <button class="btn" @click="getUserAgeFeatureStatus">Calculate Age</button>

    <p v-if="!userAgeFeature && !loading" class="text">
      Sorry, This feature has been disabled by the Admin
    </p>
    <p v-else-if="error">{error}</p>

    <div v-else-if="userAgeFeature">
      <p class="text">
        Calculate your age below by providing your year of birth
      </p>
      <input type="number" v-model="birthYear" />
      <button class="btn btn-calculate" @click="calcAge">Calculate</button>
      <button class="btn" @click="getUserAgeFeatureStatus">
        Calculate Age
      </button>
      <p v-if="age">You are {{ age }} years old</p>
    </div>
  </div>
</template>