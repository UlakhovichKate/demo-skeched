<script>
export default {
  props: ['slide'],
  emits: ['active-count', 'button-navigation'],
  data() {
    return {
      people: [
        {name: 1, price: 0, title: 'Single'},
        {name: 2, price: 2, title: 'two'},
        {name: 3, price: 4, title: 'Three'},
        {name: 4, price: 6, title: 'Four'},
        {name: 'baby', price: 0, title: 'Baby'}
      ],
      selected: false
    }
  },
  methods: {
    selectCount(el) {
      this.selected = el;
      this.$parent.$emit('active-count', this.selected);
      this.$parent.$emit('button-navigation', this.slide + 1);
    },
    createImageUrl(el) {
      let name = el.toLowerCase();
      return "/assets/peoples/" + name + ".png"
    }
  }
}
</script>

<template>
  <ul class="composition">
    <li v-for="(item, index) in people" :key="index" @click="selectCount(item)" class="composition__item" :class="{ 'js-active': selected === item.name }">
      <img :src="createImageUrl(item.title)" class="composition__img" :alt="item.name">
      <span class="composition__name">{{ item.name === 'baby' ? 'baby' : index + 1 }}</span>
    </li>
  </ul>
</template>

<style scoped>
  .composition {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: 27px 10px;
    list-style: none;
    margin: 0 auto;
    padding: 0;
  }

  .composition__item {
    max-width: 30%;
    width: 100%;
  }

  .composition__item.js-active .composition__img {
    border: 1px solid #FFBD9B;
  }

  .composition__img {
    max-width: 180px;
    width: 100%;
  }

  .composition__name {
    display: block;
    margin-top: 14px;
    font-family: 'Hatton';
    font-weight: 500;
    font-size: 16px;
    line-height: 30px;
    text-align: center;
    text-transform: uppercase;
  }
</style>
