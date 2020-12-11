<template>
  <header>
    <nav class="row">
      <div class="logo">
        <nuxt-link to="/">
          <h1>Ninata</h1>
        </nuxt-link>
      </div>

      <button class="ham-button" @click.prevent="toggleMenu">
        <div class="hamburger"><div></div></div>
      </button>

      <div class="menu-container">
        <div class="menu">
          <nuxt-link to="/my-art" @click.native="toggleMenu">My art</nuxt-link>
          <nuxt-link to="/contact-me" @click.native="toggleMenu"
            >Contact me</nuxt-link
          >
        </div>
        <a
          href="https://www.instagram.com/ninata.art/"
          target="_blank"
          class="ig-icon"
          v-html="require('~/assets/img/icon-instagram.svg?include')"
        ></a>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  methods: {
    toggleMenu(e) {
      const hamburger = document.querySelector('.hamburger')
      const menu = document.querySelector('.menu-container')
      const logo = document.querySelector('.logo')

      hamburger.classList.toggle('open')
      menu.classList.toggle('expanded')
      logo.classList.toggle('light')
    },
  },
}
</script>

<style lang="scss" scoped>
header {
  position: fixed;
  color: $black;
  padding: 10px 0;
  width: 100%;
  z-index: 99999;
  transition: all 1s ease;
  background-color: $white;

  .row {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .logo {
    line-height: 0;
    margin: 0;
    position: relative;
    z-index: 98;

    @media (max-width: $tablet-screen) {
      &.light {
        a {
          color: $white;
          transition: all 0.5s ease-in-out 0.2s;
        }
      }
    }
  }

  h1 {
    font-family: 'Sacramento';
    font-size: 2.5rem;
    margin: 0;
  }

  .ham-button {
    position: relative;
    width: 40px;
    height: 40px;
    cursor: pointer;
    border-radius: 4px;
    border: none;
    background: $trp;

    &:focus {
      outline: none;
    }
  }

  .hamburger {
    width: 100%;
    height: 100%;
    padding: 0.5em;
    display: flex;
    align-items: center;
    position: relative;
    transition: all 1s ease;
    z-index: 98;

    div {
      width: 100%;
      height: 2px;
      background-color: $black;
      position: relative;
      transition: all 0.5s ease-out;

      &::before,
      &::after {
        content: '';
        width: 100%;
        height: 2px;
        background-color: $black;
        transition: all 0.5s ease-out;
        position: absolute;
        top: -7px;
        left: 8px;
      }

      &::after {
        top: 7px;
      }
    }

    &.open {
      div {
        background-color: $white;

        &::before,
        &::after {
          background-color: $white;
          left: -8px;
        }
      }
    }
  }

  .menu-container {
    position: fixed;
    top: 0;
    right: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: $black;
    width: 30vw;
    height: 100vh;
    padding: 2em;
    transform: translateX(100%);
    transform-origin: right;
    transition: all 0.5s ease-out;
    z-index: 97;

    .menu {
      display: flex;
      flex-direction: column;
      max-width: 100%;
    }

    a {
      color: $white;
      font-size: 2.5rem;
    }

    &.expanded {
      transform: translateX(0);
    }

    .ig-icon {
      position: absolute;
      bottom: 1%;
      left: 7%;

      ::v-deep svg {
        fill: $white;
        width: 40px;
      }
    }
  }

  @media (max-width: $tablet-screen) {
    .menu-container {
      width: 100vw;

      a {
        font-size: 2rem;
      }
    }
  }
}
</style>
