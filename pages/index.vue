<template>
  <body class="bg-pink-900">

    <pageheader />

    <div v-for="article in articles" :key="article.slug" :class="'storie mx-auto w-full flex flex-autojustify-center flex-col ' + article.class">

        <div class="articleheader mt-16 mx-5 mt-10 w-3/4 lg:w-3/5">

            <h1 class="pt-4 text-5xl md:text-6xl text-gray-200 font-black"><glitchi>{{article.title}}</glitchi></h1>

            <div class="pt-4 pb-10 text-md md:text-xl text-gray-200 font-thinnest"><glitchi>{{article.title}}</glitchi></div>

        </div>
 
        <nuxt-content :document="article" class="text-gray-300 italic text-right leading-relaxed md:leading-loose tracking-narrow text-2xl md:text-3xl" />


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
    background: #831843;
}

.stories-mystic em{
    background: #eee;
    color: #831843;
    padding: .25rem .5rem
}

.stories-fresh {
    background: #077a5d;
}

.stories-fresh em{
    background: #eee;
    color: #077a5d;
    padding: .25rem .5rem
}

.stories-dark {
    background: #060219;
}

.stories-dark em{
    background: #eee;
    color: #060219;
    padding: .25rem .5rem

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