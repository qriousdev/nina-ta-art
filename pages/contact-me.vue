<template>
  <main>
    <section id="contact-form">
      <div class="row">
        <h1>Contact me</h1>
        <Contact />
      </div>
    </section>
  </main>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
#contact-form {
  padding: 60px 0 60px;

  .row {
    max-width: 600px;
    width: 80%;
  }

  h1 {
    text-align: center;
    margin-bottom: 1em;
  }
}
</style>
