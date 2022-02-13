<template>
  <v-app>
    <v-app-bar app dark class="background">
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn to="/" text>
        <span class="mr-2">Home</span>
      </v-btn>

      <v-btn to="/about" text>
        <span class="mr-2">About</span>
      </v-btn>

      <v-btn to="/product" text>
        <span class="mr-2">Product</span>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>

<style>
.background {
  background: rgb(255, 255, 255);
  animation: mymove 5s infinite;
}

@keyframes mymove {
  from {
    background-color: wheat;
  }
  to {
    background-color: rgb(241, 208, 147);
  }
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  100% {
    background-position: 100% 0%;
  }
}

.mr-2 {
  background: linear-gradient(80deg, #929292, #000000);
  background-size: 50%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: gradient 3s infinite;
}
</style>
