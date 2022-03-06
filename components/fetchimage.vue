<template>

    <div class="withborder">

        <nuxt-img 
          provider="cloudinary" 
          :src="cldimage"
          preload
          sizes="sm:100vw md:100vw lg:100vw xxl:100vw"
          dpr="auto"
          crop="fill"
          fetchFormat="auto"
          quality="auto"
          class="para"
          width="1024px"
        />      

    </div>  

</template>

<script>  
import simpleParallax from 'simple-parallax-js';

export default {

    props: ["folder", "image"],

    data () {
        return {
            cldimage: this.folder + this.image,
        }
    },

    mounted() {
        var image = document.getElementsByClassName('para');
        new simpleParallax(image, {
	        maxTransition: 80,
            delay: .6,
	        transition: 'cubic-bezier(0,0,0,1)',
            scale: 1.075,
            orientation: 'up-right'

        });
    },


};  
</script>

<style>

.withborder { 

    background-image: url(/border.png);
    background-size: 100% 100%;
    margin: .5rem;
    }
    
.withborder img {

    mix-blend-mode: darken; 

}

</style>