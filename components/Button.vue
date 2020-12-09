<template>
  <div class="button">
    <nuxt-link :to="link" :class="setclass" :target="target">
      {{ text }}
    </nuxt-link>
  </div>
</template>

<script>
export default {
  props: {
    link: {
      type: String,
      default: '',
      required: true,
    },
    setclass: {
      type: String,
      default: '',
      required: true,
    },
    text: {
      type: String,
      default: '',
      required: true,
    },
    target: {
      type: String,
      default: '_self',
      required: false,
    },
  },
}
</script>

<style lang="scss" scoped>
@mixin btn($background, $color, $border) {
  background-color: $background;
  color: $color;
  font-size: 1.3rem;
  text-align: left;
  text-decoration: none;
  padding: 0.6em 1em;
  font-weight: 400;
  letter-spacing: 1px;
  border-bottom: 2px solid $border;
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
    background-color: transparent;
    color: $black;
    border-color: $black;
  }
}
</style>
