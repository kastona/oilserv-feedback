<template>
  <v-app>



    <v-app-bar
      color="warning"
      fixed
      dark
      app
      elevate-on-scroll
    >
      <v-avatar
        size="40"
        style="cursor: pointer;"
        @click="$router.push('/')"
      >
        <v-img
          :src="require('@/assets/logo.png')"
          contain
          height="100%"


        />
      </v-avatar>

    </v-app-bar>





    
    <v-main style="background-color: #dee3f9;">
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      color="warning"
      dark
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
      <v-spacer></v-spacer>
      <span class="subtitle-1"> Oilserv Limited</span>
      <v-spacer></v-spacer>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      fixed: false,
    }
  }
}
</script>
