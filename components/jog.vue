<template>

  <span data-splitting class="headline--jog"><slot></slot></span>

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


.headline--jog {
  .char {
    --name: jog;
    --dur: 500ms;
    --del: calc(var(--char-index) * -0.025s);
    --tf: linear;
  }

  @keyframes jog {
    0% {
      transform: translate(0, 0) rotate(5deg);
    }
    25% {
      transform: translate(5%, -5%) rotate(10deg);
    }
    50% {
      transform: translate(5%, 0) rotate(15deg);
    }
    75% {
      transform: translate(10%, -5%) rotate(10deg);
    }
    100% {
      transform: translate(0, 0) rotate(5deg);
    }
  }
}


</style>