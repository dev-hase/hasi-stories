<template>
    <div class="bg-pink-700 text-center text-white p-6">
        <h1 class="text-6xl font-black tracking-narrow"><span>HASI</span></h1>
        <h3 class="text-4xl tracking-widest" style="margin-top: -.5rem;"><span>stories</span></h3>
    </div>

</template>

<style lang="stylus" scoped>

h1, h3 {
  transform: scale(0.94);
  animation: scale 3s forwards cubic-bezier(0.5, 1, 0.89, 1);
}

@keyframes scale {
  100% {
    transform: scale(1);
  }
}

span {
  display: inline-block;
  opacity: 0;
  filter: blur(4px);
}

h1 span {
  animation: fade-in 0.8s 0.1s forwards cubic-bezier(0.11, 0, 0.5, 0);
}

h3 span {
  animation: fade-in 1.8s 0.2s forwards cubic-bezier(0.11, 0, 0.5, 0);
}

@keyframes fade-in {
  100% {
    opacity: 1;
    filter: blur(0);
  }
}

</style>