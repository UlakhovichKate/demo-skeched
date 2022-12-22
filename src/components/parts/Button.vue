<script>
export default {
  props: {
    id: Number,
    name: String,
    type: String,
    slide: Number,
    class: String
  },
  emits: ['button-navigation'],
  data() {
    return {
      link: 1,
      className: '',
      activeSlide: 1
    }
  },
  methods: {
    checkTheType() {
      let addedClass = this.class ? this.class : '';
      if (this.type === 'next') {
        this.link = this.slide + 1;
        this.className = 'primary ' + addedClass;
      } else {
        this.link = this.slide - 1;
        this.className = 'secondary ' + addedClass;
      }
    },
    switchSlide() {
      this.$parent.$emit('button-navigation', this.link);
    }
  },
  mounted() {
    this.checkTheType()
  }
}
</script>

<template>
  <button class="button" :data-link="link" :class="className" type="submit" @click="switchSlide">{{ name }}</button>
</template>

<style scoped>
  .button {
    letter-spacing: .03666rem;
    margin: auto;
    max-width: 32.5rem;
    text-transform: uppercase;
    width: 100%;
    border: none;
    cursor: pointer;
    padding: 1.25rem 2rem 1.33333rem;
    border-radius: 4.16666rem;
  }

  .button:hover {
    opacity: 0.7;
  }

  .button.primary {
    background-color: #ffbd9b;
    color: #000;
  }

  .button.secondary {
    background-color: #000;
    color: #fff;
  }

  .button:not(:last-of-type) {
    margin-bottom: 10px;
  }

  .button--top-left {
    position: absolute;
    top: 30px;
    left: 30px;
    width: 40px;
    height: 40px;
    padding: 10px;
  }

  .button--confirm {
    position: absolute;
    top: 30px;
    left: calc(50% - 250px/2);
    max-width: 250px;
  }

  .button.secondary.button--top-left {
    background-color: #888;
  }
</style>
