<template>
  <main>
    <section id="control">
      <div class="row">
        <h1>My art</h1>
        <div class="container">
          <ul class="categories">
            <li
              class="show-anime"
              data-move="0px"
              data-show="anime"
              @click="selectCategory"
            >
              Anime
            </li>
            <li
              class="show-chibi"
              data-move="100px"
              data-show="chibi"
              @click="selectCategory"
            >
              Chibi
            </li>
            <li
              class="show-classical"
              data-move="200px"
              data-show="classical"
              @click="selectCategory"
            >
              Classical
            </li>
            <li
              class="show-design"
              data-move="300px"
              data-show="design"
              @click="selectCategory"
            >
              Design
            </li>
            <li
              class="show-portrait"
              data-move="400px"
              data-show="portrait"
              @click="selectCategory"
            >
              Portrait
            </li>
            <li
              class="show-style"
              data-move="500px"
              data-show="style"
              @click="selectCategory"
            >
              Style
            </li>
            <li class="line" @click="selectCategory"></li>
          </ul>
        </div>
      </div>
    </section>

    <section id="gallery">
      <div class="row">
        <div v-if="show === 'anime'" class="anime masonry">
          <div
            v-for="(img, i) in animeImgs"
            :key="i"
            class="anime-img"
            @click="lightbox"
          >
            <img :src="require(`~/assets/img/portfolio/anime/${img}`)" />
          </div>
        </div>

        <div v-if="show === 'chibi'" class="chibi masonry">
          <img
            v-for="(img, i) in chibiImgs"
            :key="i"
            :src="require(`~/assets/img/portfolio/chibi/${img}`)"
            @click="lightbox"
          />
        </div>

        <div v-if="show === 'classical'" class="classical masonry">
          <img
            v-for="(img, i) in classicalImgs"
            :key="i"
            :src="require(`~/assets/img/portfolio/classical/${img}`)"
            @click="lightbox"
          />
        </div>

        <div v-if="show === 'design'" class="design masonry">
          <img
            v-for="(img, i) in designImgs"
            :key="i"
            :src="require(`~/assets/img/portfolio/design/${img}`)"
            @click="lightbox"
          />
        </div>

        <div v-if="show === 'portrait'" class="portrait masonry">
          <img
            v-for="(img, i) in portraitImgs"
            :key="i"
            :src="require(`~/assets/img/portfolio/portrait/${img}`)"
            @click="lightbox"
          />
        </div>

        <div v-if="show === 'style'" class="style masonry">
          <img
            v-for="(img, i) in styleImgs"
            :key="i"
            :src="require(`~/assets/img/portfolio/style/${img}`)"
            @click="lightbox"
          />
        </div>
      </div>
    </section>
    <div id="lightbox" @click="disableLightbox">
      <img
        src="http://localhost:3000/app/assets/img/portfolio/anime/IMG_1990.jpeg"
      />
    </div>
  </main>
</template>

<script>
const images = {}

function importAll(r) {
  r.keys().forEach(
    (key) =>
      (images[key.substring(key.lastIndexOf('/') + 1)] = key.substring(
        key.indexOf('/') + 1,
        key.lastIndexOf('/')
      ))
  )
}

importAll(
  require.context('~/assets/img/portfolio/', true, /\.(png|jpe?g|svg)$/)
)

export default {
  data() {
    return {
      imgs: images,
      show: 'anime',
    }
  },

  computed: {
    animeImgs() {
      return Object.keys(this.imgs).filter((key) => this.imgs[key] === 'anime')
    },

    chibiImgs() {
      return Object.keys(this.imgs).filter((key) => this.imgs[key] === 'chibi')
    },

    classicalImgs() {
      return Object.keys(this.imgs).filter(
        (key) => this.imgs[key] === 'classical'
      )
    },

    designImgs() {
      return Object.keys(this.imgs).filter((key) => this.imgs[key] === 'design')
    },

    portraitImgs() {
      return Object.keys(this.imgs).filter(
        (key) => this.imgs[key] === 'portrait'
      )
    },

    styleImgs() {
      return Object.keys(this.imgs).filter((key) => this.imgs[key] === 'style')
    },
  },

  methods: {
    selectCategory(e) {
      const line = document.querySelector('.line')
      const move = e.target.dataset.move
      const show = e.target.dataset.show

      line.style.transform = `translateX(${move})`
      this.show = show
    },

    lightbox(e) {
      const lightbox = document.querySelector('#lightbox')
      const img = lightbox.querySelector('img')

      img.src = e.target.currentSrc
      lightbox.style.display = 'flex'
    },

    disableLightbox(e) {
      const lightbox = document.querySelector('#lightbox')

      if (e.target === lightbox) {
        lightbox.style.display = 'none'
      }
    },

    // resizeImg() {
    //   const masonry = document.querySelector('.masonry')
    //   const rowGap = parseInt(
    //     window.getComputedStyle(masonry).getPropertyValue('grid-row-gap')
    //   )
    //   const rowHeight = parseInt(
    //     window.getComputedStyle(masonry).getPropertyValue('grid-auto-rows')
    //   )

    //   const imgs = document.querySelectorAll('.masonry > div')

    //   imgs.forEach((img) => {
    //     const rowSpan = Math.ceil(
    //       (img.getBoundingClientRect().height + rowGap) / (rowHeight + rowGap)
    //     )

    //     img.style.gridRowEnd = `span ${rowSpan}`
    //   })
    // },
  },
}
</script>

<style lang="scss" scoped>
#control {
  padding: 60px 0 60px;

  .row {
    text-align: center;
  }

  h1 {
    text-align: center;
    font-weight: 300;
    font-size: 3.5rem;
  }

  .container {
    max-width: 600px;
    margin: auto;
  }

  .categories {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    position: relative;
    padding: 0;
  }

  li {
    list-style-type: none;
    padding: 0.5em 1em;
    cursor: pointer;
  }

  .line {
    position: absolute;
    bottom: 0;
    left: 20px;
    height: 2px;
    width: 60px;
    background-color: $black;
    padding: 0;
    transform: translateX(0);
    transition: all 0.4s cubic-bezier(0.48, 1.54, 0.4, 0.86);
  }
}

#gallery {
  padding-top: 0;

  .row {
    // column-count: 5;

    .masonry {
      display: grid;
      grid-gap: 1rem;
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      grid-auto-rows: 250px;

      img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        animation: fade 1s ease-in-out;
        cursor: pointer;
      }
    }

    @keyframes fade {
      0% {
        opacity: 0;
      }
      100% {
        opacity: 1;
      }
    }
  }
}

#lightbox {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba($black, 0.8);
  display: none;
  justify-content: center;
  align-items: center;
  padding: 3rem;
  z-index: 999999999;

  img {
    position: relative;
    display: block;
    max-height: 70vh;
    max-width: 70vw;
    animation: scale-up 0.2s linear;
  }

  @keyframes scale-up {
    0% {
      transform: scale(0.8);
      opacity: 0;
    }
    100% {
      transform: scale(1);
      opacity: 1;
    }
  }
}
</style>
