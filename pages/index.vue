<template>
  <body class="bg-pink-900">

    <pageheader />

    <div v-for="article in articles" :key="article.slug" :class="'storie mx-auto w-full flex flex-autojustify-center flex-col ' + article.class">

        <div class="articleheader mt-16 mx-5 mt-10 w-3/4 lg:w-3/5">

            <h1 class="pt-4 text-5xl md:text-6xl font-black tracking-tighter md:tracking-normal"><glitchi>{{article.title}}</glitchi></h1>

            <h2 class="pt-4 pb-10 text-md md:text-xl font-thinnest"><glitchi>{{article.description}}</glitchi></h2>

        </div>
 
        <nuxt-content :document="article" class="text-gray-100 italic font-bold text-right leading-relaxed md:leading-loose tracking-tight md:tracking-normal text-2xl md:text-3xl" />


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

body {
    word-break: break-word;
    hyphens: auto;
}

/* geteilte styles */

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
    line-height: 2rem;
    padding: .25rem;
    padding-top: .75rem;
    padding-bottom: 0;
    letter-spacing: .125rem;
    overflow: hidden;
    display: inline-block;
}

.stories-fresh p, .stories-dark p, .stories-mystic p {
    text-shadow: 1px 1px 5px #eee;
}

/* mystic */

.stories-mystic {
    background-color: #831843;
    background-image: url(/canvas.png);
    background-size: 50rem;
    background-blend-mode: multiply;
}
.stories-mystic p, .stories-mystic .articleheader{
    color: #eee;
}
.stories-mystic .articleheader{
    border-top: 3px solid #eee;
}

/* dark */

.stories-dark {
    background-color: #060219;
    background-image: url(/canvas.png);    
    background-size: 50rem;
    background-blend-mode: multiply;
}
.stories-dark p, .stories-dark .articleheader{
    color: #eee;
}
.stories-dark .articleheader{
    border-top: 3px solid #eee;
}
.stories-dark em {
    background: #f0052a;

}

/* fresh */ 

.stories-fresh {
    background-color: #a8f8d3;
    background-image: url(/canvas.png);
    background-size: 50rem;
    background-blend-mode: multiply;
}
.stories-fresh p, .stories-fresh .articleheader{
    color: #446d5b;
}
.stories-fresh .articleheader{
    border-top: 3px solid #446d5b;
}
.stories-fresh em {
    background: #446d5b;
    color: #fff;
    mix-blend-mode: darken;
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

.nuxt-content p:last-of-type {
  margin-bottom: 5rem;
}

@media screen and (min-width: 1200px) {
  .nuxt-content p {
      padding: 5rem 3rem 3.2rem 0rem;
  }
}



</style>