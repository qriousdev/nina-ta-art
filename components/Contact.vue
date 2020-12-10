<template>
  <div class="contact-me">
    <form name="contact" method="POST" data-netlify="true" action="/thank-you">
      <p>
        <label for="name">Your name</label>
        <input
          type="text"
          id="name"
          name="name"
          required
          minlength="2"
          maxlength="100"
        />
      </p>
      <p>
        <label for="email">Your email</label>
        <input
          type="email"
          id="email"
          name="email"
          required
          minlength="2"
          maxlength="100"
        />
      </p>
      <p>
        <label for="message">Message</label>
        <textarea id="message" name="message" rows="3" required></textarea>
      </p>
      <p>
        <button type="submit" class="btn-black">Send to Nina</button>
      </p>
    </form>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.contact-me {
  label {
    display: block;
    color: $dark;
  }

  input {
    display: block;
    border: none;
    border-bottom: 1px solid $black;
    padding: 1em 0 0.5em;
    font-size: 1.2rem;
    width: 100%;
    font-family: inherit;

    &:focus {
      outline: none;
    }
  }

  textarea {
    border: none;
    border-bottom: 1px solid $black;
    width: 100%;
    padding: 1em 0 0.5em;
    font-size: 1.2rem;
    font-family: inherit;

    &:focus {
      outline: none;
    }
  }

  @mixin btn($background, $color, $border) {
    background-color: $background;
    color: $color;
    font-size: 1.3rem;
    text-align: left;
    text-decoration: none;
    padding: 0.6em 1em;
    font-weight: 400;
    letter-spacing: 1px;
    border: 1px solid $border;
    transition: all 0.2s ease-in-out;
    display: inline-block;
    cursor: pointer;

    a {
      color: $color;
    }
  }

  .btn-black {
    @include btn($trp, $black, $black);

    &:hover {
      background-color: $black;
      color: $white;
      border-color: $black;
    }
  }
}
</style>
