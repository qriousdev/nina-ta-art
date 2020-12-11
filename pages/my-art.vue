<template>
  <main>
    <section id="control">
      <div class="row">
        <h1>My art</h1>
        <div id="current-category" @click="dropdown">
          <span>{{ show }}</span>
          <i>▼</i>
        </div>
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
          <img
            v-for="(img, i) in animeImgs"
            :key="i"
            :srcSet="require(`~/assets/img/portfolio/anime/${img}?size=300`)"
            :src="require(`~/assets/img/portfolio/anime/${img}`)"
            @click="lightbox"
          />
        </div>

        <div v-if="show === 'chibi'" class="chibi masonry">
          <img
            v-for="(img, i) in chibiImgs"
            :key="i"
            :srcSet="require(`~/assets/img/portfolio/chibi/${img}?size=300`)"
            :src="require(`~/assets/img/portfolio/chibi/${img}`)"
            @click="lightbox"
          />
        </div>

        <div v-if="show === 'classical'" class="classical masonry">
          <img
            v-for="(img, i) in classicalImgs"
            :key="i"
            :srcSet="
              require(`~/assets/img/portfolio/classical/${img}?size=300`)
            "
            :src="require(`~/assets/img/portfolio/classical/${img}`)"
            @click="lightbox"
          />
        </div>

        <div v-if="show === 'design'" class="design masonry">
          <img
            v-for="(img, i) in designImgs"
            :key="i"
            :srcSet="require(`~/assets/img/portfolio/design/${img}?size=300`)"
            :src="require(`~/assets/img/portfolio/design/${img}`)"
            @click="lightbox"
          />
        </div>

        <div v-if="show === 'portrait'" class="portrait masonry">
          <img
            v-for="(img, i) in portraitImgs"
            :key="i"
            :srcSet="require(`~/assets/img/portfolio/portrait/${img}?size=300`)"
            :src="require(`~/assets/img/portfolio/portrait/${img}`)"
            @click="lightbox"
          />
        </div>

        <div v-if="show === 'style'" class="style masonry">
          <img
            v-for="(img, i) in styleImgs"
            :key="i"
            :srcSet="require(`~/assets/img/portfolio/style/${img}?size=300`)"
            :src="require(`~/assets/img/portfolio/style/${img}`)"
            @click="lightbox"
          />
        </div>
      </div>
    </section>
    <div id="lightbox" @click="disableLightbox">
      <img src="" />
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
      const lis = document.querySelectorAll('.categories li')

      line.style.transform = `translateX(${move})`
      this.show = show

      if (lis[0].classList.contains('li-show')) {
        this.dropdown()
      }
    },

    lightbox(e) {
      const lightbox = document.querySelector('#lightbox')
      const img = lightbox.querySelector('img')

      img.src = e.target.attributes.src.value
      lightbox.style.display = 'flex'
    },

    disableLightbox(e) {
      const lightbox = document.querySelector('#lightbox')

      if (e.target === lightbox) {
        lightbox.style.display = 'none'
      }
    },

    dropdown() {
      const categories = document.querySelector('.categories')
      const lis = categories.querySelectorAll('li')
      const icon = document.querySelector('#current-category i')

      categories.classList.toggle('ctg-show')
      lis.forEach((li) => li.classList.toggle('li-show'))
      icon.classList.toggle('rotate')
    },
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

  #current-category {
    display: none;
  }

  .container {
    max-width: 600px;
    margin: auto;
    position: relative;
    z-index: 9;
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

  @media (max-width: 690px) {
    #current-category {
      display: inline-block;
      text-transform: capitalize;
      border-top: 1px solid $black;
      width: 150px;
      cursor: pointer;

      span {
        font-size: 1.4rem;
        margin-right: 0.5em;
        font-weight: 300;
      }

      i {
        display: inline-block;
        transform: rotate(-127deg);
        font-size: 0.8rem;
        color: $dark;
        transition: all 0.3s ease-out;

        &.rotate {
          transform: rotate(-307deg);
        }
      }
    }

    .categories {
      display: inline-block;
      width: 150px;
      border-bottom: 1px solid $black;
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-50%);
      max-height: 0vh;
      background-color: #f7f7f7;
      transition: all 0.5s ease;

      &.ctg-show {
        max-height: 200vh;
      }

      li {
        opacity: 0;
        pointer-events: none;
        transition: all 0.3s ease-out;

        &.li-show {
          position: relative;
          opacity: 1;
          pointer-events: auto;
        }
      }
    }

    .line {
      display: none;
    }
  }
}

#gallery {
  padding-top: 0;

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

  @media (max-width: $tablet-screen) {
    .masonry {
      grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
      grid-auto-rows: 150px;
      grid-gap: 0.5rem;
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

#lightbox {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba($black, 0.8);
  display: none;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 3rem;
  z-index: 999999999;

  img {
    position: relative;
    max-height: 70vh;
    max-width: 70vw;
    animation: scale-up 0.2s linear;
  }

  @media (max-width: $tablet-screen) {
    img {
      max-height: 85vh;
      max-width: 85vw;
    }
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
