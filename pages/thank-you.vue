<template>
  <main>
    <section id="hero">
      <div class="row">
        <p class="bubble">
          I received your message and will get back to your soon 🙂
        </p>
        <div
          class="chibbi"
          v-html="require('~/assets/img/nina-standing.svg?include')"
        ></div>
      </div>
    </section>
  </main>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
#hero {
  min-height: 100vh;
  padding-top: 75px;

  .row {
    text-align: center;
    position: relative;
  }

  .bubble {
    font-size: 1.2rem;
    line-height: 1.4em;
    position: relative;
    max-width: 250px;
    border-radius: 100px;
    padding: 1em;
    margin: 0 auto 2.5em;
    border: 1px solid $dark;

    &::before,
    &::after {
      content: ' ';
      position: absolute;
      left: 55px;
      bottom: -30px;
      width: 40px;
      height: 40px;
      background-color: #fff;
      border-radius: 28px;
      border: 1px solid $dark;
    }

    &::after {
      width: 20px;
      height: 20px;
      left: 80px;
      bottom: -40px;
      border-radius: 18px;
    }

    @media (max-width: $mobile-screen) {
      font-size: 1rem;
    }
  }

  .chibbi {
    ::v-deep svg {
      height: 50vh;
    }
  }
}
</style>
