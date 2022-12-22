<script>
import Counter from "./parts/Counter.vue";

export default {
  components: {Counter},
  emits: ['variations-count'],
  data() {
    return {
      sizes: [
        {title: 'A4', name: 'a4', description: '210mm x 297 mm', price: 18.00, count: 0},
        {title: 'A5', name: 'a5', description: '148mm x 210 mm', price: 15.00, count: 0}
      ],
      isSelected: false
    }
  },
  watch: {
    sizes: {
      handler: function (val, oldVal) {
        this.$parent.$emit('variations-count', val);

        let arr = [];

        val.forEach(el => {
          if (el.count > 0) {
            arr.push(el);
          }
        });

        this.isSelected = arr.length > 0;
      },
      deep: true,
    }
  }
}
</script>

<template>
  <ul class="sizes">
    <li class="sizes__item" v-for="item in sizes" :key="item.name">
      <h3 class="sizes__title">{{ item.title }}</h3>
      <div class="sizes__description">{{ item.description }}</div>
      <div class="sizes__price">£ {{ item.price }}</div>

      <Counter :variation="item.name" @var-count="(k)=>{item.count = k}"/>

    </li>
  </ul>
</template>

<style>
.sizes {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: center;
  gap: 30px;
  list-style: none;
  padding: 0;
}


.sizes__item {
  margin-bottom: 30px;
}

.sizes__title {
  margin-bottom: 6px;
  font-size: 24px;
  text-transform: uppercase;
 }

.sizes__description,
.sizes__description p {
  margin-bottom: 6px;
  font-size: 12px;
  color: #99715D;
}

.sizes__price {
  margin-bottom: 8px;
  font-size: 14px;
  font-weight: 500;
}

.sizes__item--sale {
   margin-bottom: 32px;
   background-color: #fff;
   padding: 32px;
 }

</style>
