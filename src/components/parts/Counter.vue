<script>
export default {
  emits: ['var-count'],
  props: ['variation'],
  data() {
    return {
      count: 0,
    }
  },
  methods: {
    doCount(type) {
      if (type === 'more') {
        this.count++;
      } else {
        this.count--;
        this.count = this.count < 0 ? 0 : this.count;
      }

      this.$emit('var-count', this.count);
    },
  }
}
</script>

<template>
  <div class="sizes__counter" :data-variation="variation">
    <button class="counter-minus" @click="doCount('less')">-</button>
    <div class="counter-display">{{ count }}</div>
    <button class="counter-plus" @click="doCount('more')">+</button>
  </div>
</template>

<style>


.sizes__counter {
  width: 140px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: auto;
  padding: 6px 12px;
  border: 1px solid #FFBD9B;
  border-radius: 30px;
}
.counter-minus,
.counter-plus {
   width: 30px;
   padding: 6px;
   color: #FFBD9B;
   font-size: 18px;
  background: transparent;
  border: none;
  cursor: pointer;
}

.counter-minus:hover,
.counter-plus:hover {
  color: #99715D;
}

</style>
