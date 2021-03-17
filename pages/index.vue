<template>

  <div>


    <section class="welcome-background">

      <v-container style="min-height: 50vh;" fluid fill-height>
        <v-layout flex align-center justify-center>
          <v-flex class="white--text text-center" xs12 md8 sm6>
              <h2 class=" display-2 font-weight-bold mb-3">
                Oilserv Feedback Platform</h2>

              <v-responsive
                 class="mx-auto title font-weight-light mb-4"
                max-width="720"
              >
                You are completely anonymous, so don't hold back.
              </v-responsive>

          </v-flex>
        </v-layout>
      </v-container>
    </section>



  <v-row class="mt-n12 mb-8">
    <v-col cols="12" md="8" offset-md="2">
      <v-card elevation="20" class="pb-10">
        
        <v-card-text>
          <v-form ref="form">
            <v-card
              v-for="(fq, i) in feedbackQuestions"
              :key="i"
              flat
            >
              <v-card-title class="pb-0">{{ fq.question }}</v-card-title>
              <v-card-text style="margin-left: 20px">
                <v-expansion-panels

                  flat
                  readonly
                  :value="fq.radioModel ? 0 : 1"
                  :hide-actions="true"
                >
                  <v-expansion-panel>
                    <v-expansion-panel-header class="py-0">
                      <v-radio-group v-model="fq.radioModel" row>
                        <v-radio :label="fq.yesLabel" :value="true"></v-radio>
                        <v-radio :label="fq.noLabel" :value="false"></v-radio>
                      </v-radio-group>
                    </v-expansion-panel-header>
                    <v-expansion-panel-content>
                      <v-textarea
                        filled
                        auto-grow
                        rows="2"
                        color="warning"
                        :label="fq.answerLabel"
                        v-model="fq.answer"
                        required
                      ></v-textarea>
                    </v-expansion-panel-content>
                  </v-expansion-panel>
                </v-expansion-panels>
              </v-card-text>
              <v-divider></v-divider>
            </v-card>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            :disabled="!answeredAtleastOne || loading"
            @click="postFeedback"
            color="warning"
            rounded
            :loading="loading"
            >Submit Feedback</v-btn
          >
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
  </div>
</template>


<script>
import { mapGetters, mapActions } from "vuex";

export default {
  data: () => ({
    dealtWithOilserv: false,
    loading: false,

    feedbackQuestions: [
      {
        question: "Have you had any business with Oilserv in the past?",
        radioModel: false,
        yesLabel: "Yes",
        noLabel: "No",
        answerLabel:
          "How would you rate your overall satisfaction with Oilserv?",
        answer: "",
      },

      {
        question: "What do you like best about Oilserv?",
        radioModel: false,
        yesLabel: "Let me share",
        noLabel: "I'll pass",
        answerLabel: "Your answer",
        answer: "",
      },
      {
        question: "Kindly share a few things we could do better.",
        radioModel: false,
        yesLabel: "I'll me share",
        noLabel: "I'll pass",
        answerLabel: "Your comment",
        answer: "",
      },

      {
        question: "Do you have any more comments or questions?",
        radioModel: false,
        yesLabel: "Yes",
        noLabel: "No",
        answerLabel: "Please kindly share them here.",
        answer: "",
      },
    ],
  }),
  components: {},

  methods: {
    ...mapActions({}),

    async postFeedback() {
      this.loading = true;
      await this.$axios.post(
        "https://oilserv-feedback-backend.herokuapp.com/feedbacks",
        this.feedbackQuestions
      );

      this.loading = false;
    },
  },
  computed: {
    ...mapGetters({}),
    openValue(fq) {
      if (fq.radioModel) {
        return 0;
      }
    },

    answeredAtleastOne() {
      let found = this.feedbackQuestions.find((fq) => {
        return fq.radioModel && fq.answer.length > 1;
      });

      if (found) {
        return true;
      }
      return false;
    },
  },

  mounted() {},
};
</script>

<style scoped>
 .welcome-background {
    background-image: linear-gradient(#fb8c00, #ad6103f6);
    
  }




.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
