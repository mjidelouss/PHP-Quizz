<template>
  <v-app>
    <v-main>
      <StepperComponent />
    </v-main>
  </v-app>
</template>

<script>
import StepperComponent from './components/StepperComponent.vue';

export default {
  name: 'App',

  components: {
    StepperComponent,
  },

  data: () => ({
    
  }),
  
};
</script>
