<script>
  export default {
    props: {
      length: Number,
      active: Number
    },
  }
</script>

<template>
  <ul class="pagination">
    <li v-for="n in length" class="pagination__dot" :class="{'active': n-1 === active }" :data-slide="n-1"></li>
  </ul>
</template>

<style>
  .pagination {
    align-items: center;
    display: flex;
    justify-content: center;
    margin-bottom: 4.58333rem;
    padding: 0;
    position: relative;
    list-style: none;
  }

  .pagination__dot {
    background-color: #fff2eb;
    border: 1px solid #ffbd9b;
    border-radius: 4.16666rem;
    height: 1rem;
    position: relative;
    width: 1rem;
  }

  .pagination__dot.active:after {
    background-color: #ffbd9b;
    border-radius: 4.16666rem;
    content: "";
    display: block;
    height: 0.66666rem;
    left: 0.08333rem;
    position: absolute;
    top: 0.08333rem;
    width: 0.66666rem;
  }

  .pagination__dot:not(:first-of-type) {
    margin-left: 1rem;
  }

  .pagination__dot:not(:first-of-type):before {
    background-color: #ffbd9b;
    content: "";
    display: block;
    height: 0.08333rem;
    left: -1.08333rem;
    position: absolute;
    top: 0.33333rem;
    width: 1rem;
  }
</style>
