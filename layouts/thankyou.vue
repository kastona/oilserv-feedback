<template>
  <v-app>



    <v-app-bar
      color="#c9c9c9"
      fixed
      dark
      app
      elevate-on-scroll
      shrink-on-scroll
      dense
    >
      <v-avatar
        
        style="cursor: pointer;"
        @click="$router.push('/')"
      >
        <v-img
          :src="require('@/assets/logo.png')"
          contain
          height="100%"


        />
      </v-avatar>
      <v-toolbar-title class="ml-3" @click="$router.push('/')">Oilserv Limited</v-toolbar-title>

    </v-app-bar>





    
    <v-main style="background-color: #c9c9c9;">
        <nuxt />
    </v-main>
    <v-footer
      :absolute="!fixed"
      color="#c9c9c9"
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


<style scoped>
 .background{
    background-image: linear-gradient(#fb8c00, #ad6103f6);
    
  }

</style>
