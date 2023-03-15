<script setup>
import { defineProps} from 'vue'
let result  = defineProps(['result'])
</script>

<template>
    <div>
      <!-- SCORE CONTAINER -->
      <div class="container d-flex justify-content-center">
        <div class="text-center mt-3 p-5 rounded" style="width: 500px;">
            <div>
                <div class="d-flex-block">
                  <p class="fs-2 ms-2">🎁🎁</p>
                    <h3 class="fw-bold">✨ RESULTS ✨</h3><hr>
                </div>
                <div class="box-item d-flex p-1">
                    <p class="box-para fw-bold">Score 🎯 :</p>
                    <h4 class="box-text ms-3 mt-1 fw-bold" id="score">{{ result.result.score }}</h4>
                  </div>
                  <div class="box-item d-flex">
                    <p class="box-para fw-bold">Correct Questions ✔️ :</p>
                    <h4 class="box-text ms-3 mt-1 fw-bold" id="numCorrect">{{ (result.result.score) / 100 }}</h4>
                  </div>
                  <div class="box-item d-flex">
                    <p class="box-para fw-bold">Incorrect Questions ❌ :</p>
                    <h4 class="box-text ms-3 mt-1 fw-bold" id="numIncorrect">{{ (result.result.total) - (result.result.score) / 100 }}</h4>
                  </div>
                  </div>
            </div>
          </div>
    </div>
</template>
    
<style lang="scss">

</style>