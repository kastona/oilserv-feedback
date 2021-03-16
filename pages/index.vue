<template>
  <v-row>
    <v-col cols="12" md="8" offset-md="2">
      <v-card>
        <v-card-title class="text-center darken-1">
          <span class="headline warning--text">Feedback</span>
        </v-card-title>
        <v-divider></v-divider>
        <v-card-text>
          <v-form ref="form" v-model="valid">
            <v-card
              style="margin-bottom: 10px; padding: 20px"
              v-for="(fq, i) in feedbackQuestions"
              :key="i"
            >
              <v-card-title>{{ fq.question }}</v-card-title>
              <v-card-text style="margin-left: 20px">
                <v-expansion-panels
                  flat
                  readonly
                  :value="fq.radioModel ? 0 : 1"
                  :hide-actions="true"
                >
                  <v-expansion-panel>
                    <v-expansion-panel-header>
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
            </v-card>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            :disabled="!answeredAtleastOne"
            @click="postFeedback"
            color="warning"
            >Submit Feedback</v-btn
          >
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>


<script>
import { mapGetters, mapActions } from "vuex";

export default {
  data: () => ({
    dealtWithOilserv: false,

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
        question: "Do you have anymore comments or questions?",
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
      await this.$axios.post(
        "http://localhost:4000/feedbacks",
        this.feedbackQuestions
      );
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
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
