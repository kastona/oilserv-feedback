<template>
  <v-container class="fill-height" fluid>
    <v-row align="center" justify="center">
      <v-col cols="10">
        <v-card style="height: 80vh" class="text-center elevation-12">
          <v-card-text style="padding-top: 35vh;">
              
            <h2 class="display-2 font-weight-bold mb-3">Thank You!</h2>
            <v-responsive class="mx-auto title mb-4" max-width="720">
              We appreciate your feedback.
            </v-responsive>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
import { mapGetters, mapActions } from "vuex";

export default {
  layout: "thankyou",
  data: () => ({}),
  components: {},

  methods: {
    ...mapActions({}),
  },
  computed: {
    ...mapGetters({}),
  },

  mounted() {},
};
</script>
