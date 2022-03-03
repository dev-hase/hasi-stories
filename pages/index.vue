<template>
  <body class="bg-pink-900">

    <pageheader />

    <div v-for="article in articles" :key="article.slug" :class="'storie mx-auto w-full flex flex-autojustify-center flex-col ' + article.class">

        <div class="articleheader mt-16 mx-5 mt-10 w-3/4 lg:w-3/5">

            <h1 class="pt-4 text-5xl md:text-6xl text-gray-200 font-black"><glitchi>{{article.title}}</glitchi></h1>

            <h2 class="pt-4 pb-10 text-md md:text-xl text-gray-200 font-thinnest"><glitchi>{{article.description}}</glitchi></h2>

        </div>
 
        <nuxt-content :document="article" class="text-gray-100 italic font-bold text-right leading-relaxed md:leading-loose tracking-narrow text-2xl md:text-3xl" />


    </div>

    <infinite-loading spinner="waveDots" @infinite="infiniteHandler">
      <div slot="no-more">
        <pageheader />
      </div>
      <div slot="no-results">nix gefunden</div>
    </infinite-loading>

  </body>
</template>

<script>

export default {

    data() {
        return {
            articles: [],
            pointer: 0,
            numberofarticles: 1,
        };
    },
    methods: {
        infiniteHandler($state) {
            //alert(this.pointer);
            setTimeout(async () => {
                this.newarticles = await this.$content("stories")
                    .limit(this.numberofarticles)
                    .skip(this.pointer)
                    .sortBy("slug", "desc")
                    .fetch()
                    .then((newarticles) => {
                    if (newarticles.length > 0) {
                        this.articles.push(...newarticles);
                        this.pointer += this.numberofarticles;
                        $state.loaded();
                        return { pointer, articles };
                    }
                    else {
                        $state.complete();
                    }
                });
            }, 750);
        }
    },

}

</script>

<style>

html {
    background: #831843;
}

.stories-mystic {
    background-color: #831843;
    background-image: url(/canvas.png);
    background-size: 50rem;
    background-blend-mode: multiply;
}


.stories-dark {
    background-color: #060219;
    background-image: url(/canvas.png);    
    background-size: 50rem;
    background-blend-mode: multiply;

}


.stories-fresh {
    background-color: #077a5d;
    background-image: url(/canvas.png);
    background-size: 50rem;
    background-blend-mode: multiply;
}

.stories-fresh p, .stories-dark p, .stories-mystic p {

text-shadow: 0 0.1em 20px rgba(0, 0, 0, 1), 0.05em -0.03em 0 rgba(0, 0, 0, 1),
    0.05em 0.005em 0 rgba(0, 0, 0, 1), 0em 0.08em 0 rgba(0, 0, 0, 1),
    0.05em 0.08em 0 rgba(0, 0, 0, 1), 0px -0.03em 0 rgba(0, 0, 0, 1),
    -0.03em -0.03em 0 rgba(0, 0, 0, 1), -0.03em 0.08em 0 rgba(0, 0, 0, 1), -0.03em 0 0 rgba(0, 0, 0, 1) !important;

}

.stories-fresh em, .stories-dark em, .stories-mystic em {
    background: #f5fba5;
    color: #000;
    text-shadow: none;
    mix-blend-mode: screen;
    font-size: 2rem;
    border-radius: .125rem;
    text-transform: uppercase;
    font-family: "Luckiest Guy";
    font-style: normal;
    line-height: 3.5rem;
    padding: .5rem;
    padding-top: .75rem;
    padding-bottom: 0;
    letter-spacing: .125rem;
}

.storie {
    padding: 0 .25rem;
}

@media screen and (min-width: 640px) {

  .storie {
      padding: 0 7.5vw;
  }

}

@media screen and (min-width: 1200px) {

  .storie {
      padding: 0 22.5%;
  }

}

.articleheader {
    border-top: 3px solid #eee;
    height: 40vh;
}
.nuxt-content p {
    padding: 7.5rem 2rem 3.2rem 2rem;
    margin-left: 20vw;
}

@media screen and (min-width: 1200px) {
  .nuxt-content p {
      padding: 5rem 3rem 3.2rem 0rem;
  }
}



</style>