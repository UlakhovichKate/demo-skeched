<script>
export default {
  props: ['count'],
  data() {
    return {
      currentPosition: 1
    }
  },
  methods: {
    countToNumber(el) {
      return el === 'baby' ? 1 : el;
    },
    createImageUrl(i, j) {
      let name = '';

      if (i < j) {
        name = 'right';
      } else if (i === j) {
        name = 'selected';
      } else {
        name = 'left';
      }
      return "/assets/svg/person-" + name + ".svg"
    },
    setActivePosition(el) {
      this.currentPosition = el;
    }
  }
}
</script>

<template>
  <div class="panel__positions positions">
    <button v-for="i in countToNumber(count.name)" type="button" class="positions__button" :class="{'js-active' : i === currentPosition}" :data-position="i" @click="setActivePosition(i)">
      <img v-for="j in countToNumber(count.name)" :alt="j" :src="createImageUrl(i, j)" class="positions__svg">
      <span class="positions__name">Person {{ i }}</span>
    </button>
  </div>
</template>

<style scoped>
  .positions {
    display: flex;
    flex-wrap: nowrap;
    gap: 20px;
    padding: 6px 15px 18px;
    overflow-x: scroll;
  }

  .positions__button {
    position: relative;
    min-width: 90px;
    padding: 10px 2px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: transparent;
    border: none;
    opacity: 0.5;
  }

  .positions__button.js-active,
  .positions__button:hover {
    opacity: 1;
  }

  .positions__button.js-active::after,
  .positions__button:hover::after {
    content: '';
    position: absolute;
    bottom: -10px;
    left: calc(50% - 2px);
    display: block;
    margin: 10px auto 0;
    width: 5px;
    height: 5px;
    border-radius: 50%;
    background: #FFBD9B;
  }

  .positions__name {
    padding-left: 6px;
    font-family: 'Roboto', sans-serif;
    font-size: 11px;
    line-height: 12px;
    letter-spacing: 0.04em;
    text-transform: uppercase;
  }
</style>
