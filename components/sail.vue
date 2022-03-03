<template>

  <span data-splitting class="headline--sail"><slot></slot></span>

</template>

<script>

import "splitting/dist/splitting.css";
import "splitting/dist/splitting-cells.css";
import Splitting from "splitting";

export default {

    mounted() {
        Splitting();
    }
}
</script>

<style lang="scss" scoped>

.word,
.char {
  animation-delay: var(--del);
  animation-direction: var(--dir, normal);
  animation-duration: var(--dur);
  animation-iteration-count: var(--it, infinite);
  animation-name: var(--name);
  animation-timing-function: var(--tf);
  animation-fill-mode: var(--fill, forwards);
  display: inline-block;
  position: relative;
  transform-origin: 50% 100%;
  z-index: 1;
}


// =========================
// Headline animations
// =========================

.headline--sail {
  .word {
    --dur: 5s;
    
    &:before,
    &:after {
      animation: wave var(--dur) linear infinite;
      background-image: 
        radial-gradient(
          circle at 20px -30px,
          transparent 40px,
          var(--color) 41px
        );
      background-repeat: repeat-x;
      background-size: 40px 100%;
      content: '';
      height: 150%;
      left: 0;
      position: absolute;
      top: 90%;
      width: 200%;
      z-index: 2;
    }  
    
    &:after {
      animation-duration: calc(var(--dur) * 1.4);
      opacity: 0.8;
      top: 70%;
    }
  }
  
  .char {
    --name: sail;
    --del: calc(var(--char-index) * -0.15s);
    --tf: linear;
  }
  
  @keyframes sail {
    25% { transform: rotate(-1deg) translateY(2%); }
    50% { transform: rotate(0) translateY(0); }
    75% { transform: rotate(1deg) translateY(1%); }
  }
  
  @keyframes wave {
    to { transform: translateX(-200px); }
  }
}

</style>
