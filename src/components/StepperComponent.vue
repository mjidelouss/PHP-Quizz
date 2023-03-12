<script>
import RulesComponent from './RulesComponent.vue';
import QuizzComponent from './QuizzComponent.vue';
import ScoreComponent from './ScoreComponent.vue';
  export default {
    components: {
    RulesComponent,
    QuizzComponent,
    ScoreComponent,
  },
    data() {
        return {
            e1: 1,
        };
    },
    methods: {
      
    },
}
</script>

<template>
  <v-stepper v-model="e1">
    <v-stepper-header>
      <v-stepper-step :complete="e1 > 1" step="📜">RULES</v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step :complete="e1 > 2" step="⏳">QUIZ</v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step step="🎯">SCORE</v-stepper-step>
    </v-stepper-header>

    <v-stepper-items>
      <v-stepper-content step="1">
        <v-card
          class="mb-12"
          color="light-blue lighten-5"
          height="450px"
        >
        <RulesComponent/>
      </v-card>

        <v-btn
          color="primary"
          @click="e1 = 2"
        >
          Continue
        </v-btn>

        <v-btn text>Cancel</v-btn>
      </v-stepper-content>

      <v-stepper-content step="2">
        <v-card
          class="mb-12"
          color="grey lighten-1"
          height="480px"
        >
        <QuizzComponent/>
      </v-card>

        <v-btn
          color="primary"
          @click="e1 = 3"
        >
          Continue
        </v-btn>

        <v-btn text>Cancel</v-btn>
      </v-stepper-content>

      <v-stepper-content step="3">
        <v-card
          class="mb-12"
          color="grey lighten-1"
          height="200px"
        >
        <ScoreComponent/>
      </v-card>

        <v-btn
          color="primary"
          @click="e1 = 1"
        >
          Continue
        </v-btn>

        <v-btn text>Cancel</v-btn>
      </v-stepper-content>
    </v-stepper-items>
  </v-stepper>
</template>

<style lang="scss">

</style>