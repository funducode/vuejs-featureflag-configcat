<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import TheWelcome from "./components/TheWelcome.vue";
import CalculateAge from "./components/CalculateAge.vue";
</script>

<template>
  <header>
    <!-- <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
    /> -->
    <div class="wrapper">
      <calculate-age />
    </div>
    <!-- 
    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div> -->
  </header>

  <main>
    <!-- <TheWelcome /> -->
  </main>
</template>

<style>
@import "./assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>


<script>
import * as configCat from "configcat-js";

export default {
  name: "App",
  data() {
    return {
      userAgeFeature: null,
      error: null,
      birthYear: "",
      age: "",
      loading: true,
    };
  },

  methods: {
    // Get feature status from ConfigCat
    async getUserAgeFeatureStatus() {
      try {
        // Seeing all log messages makes the first integration easier. When the integration is done you can remove this line to avoid too detailed logging in your application.
        let logger = configcat.createConsoleLogger(3); // Setting log level to 3 (Info)

        let configCatClient = configcat.createClient(
          "BwPaCO2USkqGz554uC6qeA/578pqJ9x7UiB973ct1ttCw",
          {
            // <-- This is the actual SDK Key for your Production environment
            logger: logger,
          }
        );

        const res = await configCatClient.getValueAsync(
          "calculateuseragefeature",
          false
        );

        this.userAgeFeature = res;
      } catch (err) {
        this.error = err.message;
      }

      this.loading = false;
    },

    // Calculate age
    calcAge() {
      const age = 2021 - this.birthYear;
      this.age = age;
      this.birthYear = "";
    },
  },
};
</script>
