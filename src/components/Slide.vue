<script>
import Pagination from './parts/Pagination.vue'
import Button from './parts/Button.vue'

import SlideIntro from "./SlideIntro.vue";
import SlideComposition from "./SlideComposition.vue";
import SlideGreeting from "./SlideGreeting.vue";
import SlideBuilder from "./SlideBuilder.vue";
import SlideQuantity from "./SlideQuantity.vue";
import SlideMessage from "./SlideMessage.vue";
import SlideTotal from "./SlideTotal.vue";

export default {
  components: {
    Pagination,
    Button,
    SlideIntro,
    SlideGreeting,
    SlideComposition,
    SlideBuilder,
    SlideQuantity,
    SlideMessage,
    SlideTotal
  },
  props: {
    id: Number,
    classname: String,
    title: String,
    description: String,
    buttons: Array,
    content: Object,
    isTotal: Boolean,
    pagination: Number,
    active: Number,
    selectedComposition: Object,
    selectedVariations: Object,
    addMessage: String
  },
}
</script>

<template>
  <div class="slide" :class="[classname, { 'js-active': active === id }]" :data_slide="id">
    <div class="slide__inner">

      <div class="slide__header">
        <Pagination :length="pagination" :active="active" />
        <h3 class="slide__title">{{ title }}</h3>
        <div class="slide__description" v-html="description"></div>
      </div>

      <component
              v-bind:is="content"
              class="slide__content"
              :slide="id"
              :selectedComposition="selectedComposition"
              :selectedVariations="selectedVariations"
              :addMessage="addMessage"
      ></component>

      <div class="slide__buttons">
        <Button
            v-for="button in buttons"
            :key="button.id"
            :name="button.name"
            :type="button.type"
            :slide="id"
            :class="button.class"
        />
      </div>
    </div>
  </div>
</template>

<style>
  .slide {
    background-color: #fff2eb;
    height: 100%;
    min-height: calc(100vh - 60px);
    align-items: center;
    display: none;
    flex-direction: column;
    justify-content: center;
  }

  .slide__inner {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    min-height: calc(100vh - 60px);
    height: 100%;
    padding: 40px 15px 30px;
    margin-left: auto;
    margin-right: auto;
    max-width: 800px;
    text-align: center;
  }

  .slide__title {
    font-family: 'Hatton';
    font-size: 3.33333rem;
    font-style: normal;
    font-weight: 400;
    line-height: 3.33333rem;
    margin: 0 auto 1.83333rem;
    max-width: 26.66666rem;
    text-transform: uppercase;
    width: 100%;
  }

  .slide__description {
    font-size: 1.33333rem;
    line-height: 2rem;
    margin-bottom: 3.33333rem;
  }

  .slide p {
    margin-bottom: 10px;
  }

  .slide.js-active {
    display: block;
  }

  .slide__buttons {
    position: unset;
  }
</style>
