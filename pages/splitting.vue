<template>

<main class="container">

    <sail class="headline">sail</sail>

    <yell class="headline">yell</yell>

    <jump class="headline">jump</jump>

    <jog class="headline">jog</jog>

    <splitting class="headline" action="jog">sp jog</splitting>


</main>

</template>

<script>

</script>

<style lang="scss" scoped>
$colors: #f9ca24, #3498db, #ff7979, #1abc9c, #e74c3c, #f8c291;

* {
  box-sizing: border-box;
}

html, body {
  height: 100%;
}

.container {
  max-height: 100vh;
	overflow-y: scroll;
  position: relative;
  scroll-snap-type: y mandatory;
  -webkit-overflow-scrolling: touch;
}

.headline {
  align-items: center;
  background-color: var(--color);
  display: flex;
  font-family: 'Lexend Deca', sans-serif;
  font-weight: 700;
  font-size: calc(1rem + 15vmin);
  height: 100vh;
  justify-content: center;
  overflow: hidden;
  perspective: 1000px;
  scroll-snap-align: start;
  width: 100vw;
  
  @for $i from 1 through length($colors) {
    &:nth-child(#{$i}) {
      --color: #{nth($colors, $i)};
    }
  }
}


</style>
