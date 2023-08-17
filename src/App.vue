<template>
  <main>
    <div class="advice">

      <h1 class="advice__title">Advice #{{ adviceID }}</h1>
      
      <p class="advice__content">{{ advice }}</p>
      
      <picture class="advice__divider">
        <source 
        srcset="./assets/images/pattern-divider-desktop.svg"
        media="(min-width: 800px)">

        <img src="./assets/images/pattern-divider-mobile.svg" 
            alt="Image that devides the quote andd the button to generate another quote">
      </picture>

      <button class="button" @click="getAdvice">
        <img src="./assets/images/icon-dice.svg" 
            alt="Image that devides the quote andd the button to generate another quote">
      </button>
      
    </div>
    
  </main>
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        advice: '',
        adviceID: 0,
      }
    },
    mounted() {
      this.getAdvice()
    },
     methods: {
      async getAdvice() {
        let randNum = Math.floor( Math.random() * 224); //Setting the max to 224
        await axios.get(`https://api.adviceslip.com/advice/${randNum}`)
          .then(response => {
            console.log(response)
            this.adviceID = response.data.slip.id;
            this.advice = response.data.slip.advice;
          })
          .catch(error => {
            console.log(error);
        });
      }
     }
  }
</script>