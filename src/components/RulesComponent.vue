<script>
    export default {
      data () {
        return {
        }
      },
    }
</script>

<template>
  <div>
   <h1 class="display-2 lh-1 text-center fw-bold" style="margin-top: 2rem; color: rgb(127, 127, 211);">PHP Knowledge Test</h1>
        <div class="mt-4" id="container">
            <div class="ms-4" id="">
                  <h2 class="text-center fw-bold text-danger mt-2">RULES</h2>
                  <h5 class="text-black text-center fw-bold mt-2">🌟 The contestant have to answer 12 Questions in PHP.</h5>
                  <h5 class="text-black text-center fw-bold">🌟 Each question has a time limit of 30 seconds</h5>
                  <h5 class="text-black text-center fw-bold">🌟 With each correct question you get points.</h5>
                  <h5 class="text-center text-black fw-bold mt-2">✨ Good Luck ✨</h5>
            </div>
        <img id="quiz" style="margin-left: 20rem;" src="../assets/quizz.png" alt="" height="400" width="510">
        </div>
      </div>
</template>
    
<style lang="scss">
  #container {
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  
  h1, p {
    margin-right: 20px;
  }
  
  #quiz {
    float: right;
  }
</style>