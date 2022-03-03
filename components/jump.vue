<template>

  <span data-splitting class="headline--jump"><slot></slot></span>

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


.headline--jump {
  .char {
    --name: jump;
    --dur: 800ms;
    --del: calc(var(--char-index) * 0.075s);
    --tf: cubic-bezier(0.165, 0.44, 0.64, 1);
  }

  @keyframes jump {
    20% {
      transform: translateY(2%) scaleY(0.9);
    }
    40% {
      transform: translateY(-100%) scaleY(1.2);
    }
    50% {
      transform: translateY(10%) scaleY(0.8);
    }
    70% {
      transform: translateY(-5%) scaleY(1);
    }
    80%, 100% {
      transform: translateY(0) scaleY(1);
    }
  }
}


</style>
