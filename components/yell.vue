<template>

  <span data-splitting class="headline--yell"><slot></slot></span>

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


.headline--yell {
  .char {
    --name: yell;
    --dur: 3s;
    --tf: ease;
    
    transform-origin: 50% 100%;
  }
  
  @keyframes yell {
    3% {
      transform:
        scale(calc(1 * var(--distance-percent) + 1.5)) 
        rotate(calc(15deg * var(--distance-sine)))
        translateY(-10%);
    }
    6% {
      transform:
        scale(calc(1 * var(--distance-percent) + 1.2)) 
        rotate(calc(15deg * var(--distance-sine)))
        translateY(-10%);
    }
    12% {
      transform:
        scale(calc(1 * var(--distance-percent) + 1.5)) 
        rotate(calc(15deg * var(--distance-sine)))
        translateY(-10%);
    }
    18% { transform: scaleY(1) translateY(-2%); }
    25% { transform: scaleY(0.98); }
    50% { transform: scaleY(1); }
    75% { transform: scale(0.98); }
  }
}

</style>