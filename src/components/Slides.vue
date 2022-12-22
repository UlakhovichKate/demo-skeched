<script>
import Slide from './Slide.vue';

export default {
  components: {
    Slide
  },
  data() {
    return {
      currentTab: 'SlideIntro',
      tabs: ['SlideIntro', 'SlideGreeting', 'SlideComposition', 'SlideBuilder', 'SlideQuantity', 'SlideMessage', 'SlideTotal'],
      isActive: 0,
      activeCount: '',
      variations: [{name: false, quantity: 0}],
      message: '',
      slides: [
        {
          classname: 'intro',
          title: 'Create a card',
          description: '<p>Welcome to our brand new bespoke card builder. Here you can choose from a range of hand drawn options to create your own Sketched by Siena design. These are available either as an A5 greeting card or and A4 watercolour sheet, perfect for framing! Follow the selection options below to build your card, selecting the character and their outfits and accessories, before adding the background, props and a personalised message.</p><p>The Sketched by Siena brush is in your hand now!</p>',
          buttons: [
              {id: 1, type: 'next', name: 'Start your design!'},
            ],
          content: false
        },
        {
          classname: 'greeting',
          title: 'Your card title',
          description: '<p>Add a message to the card, choose from one of our options or write your own.</p>',
          buttons: [
              {id: 1, type: 'next', name: 'NEXT STEP'},
              {id: 2, type: 'back', name: 'Back'},
            ],
          content: 'SlideGreeting'
        },
        {
          classname: 'composition',
          title: 'number of people',
          description: '<p>Choose the number of adults on your card. You’ll be able to add a pet or a child later on.</p>',
          buttons: [
              {id: 1, type: 'back', name: 'Back'},
            ],
          content: 'SlideComposition'
        },
        {
          classname: 'builder',
          title: '',
          description: '',
          buttons: [
              {id: 1, type: 'next', name: 'confirm this design', class: 'button--confirm'},
              {id: 2, type: 'back', name: '<', class: 'button--top-left'},
            ],
          content: 'SlideBuilder'
        },
        {
          classname: 'size-quantity',
          title: 'size & quantity',
          description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce a dui in.',
          buttons: [
              {id: 1, type: 'next', name: 'NEXT'},
              {id: 2, type: 'back', name: 'back'},
            ],
          content: 'SlideQuantity'
        },
        {
          classname: 'message',
          title: 'Personalise',
          description: 'Write a personalised message on the inside of the card (able only for A5 Greeting card)',
          buttons: [
              {id: 1, type: 'next', name: 'ADD (or Skip and leave the empty)'},
              {id: 2, type: 'back', name: 'Back'},
            ],
          content: 'SlideMessage'
        },
        {
          classname: 'total',
          title: '',
          description: '',
          buttons: [
              {id: 1, type: 'back', name: '<', class: 'button--top-left'},
            ],
          content: 'SlideTotal',
          isTotal: true
        }
      ]
    }
  },
}
</script>

<template>

  <Slide
      v-for="(slide, index) in slides"
         :key="index"
         :id="index"
         :title="slide.title"
         :description="slide.description"
         :buttons="slide.buttons"
         :content="slide.content"
         :isTotal="slide.isTotal"
         :classname="[slide.classname]"
         :pagination="slides.length"
      @button-navigation="(i)=>{isActive = i}"
      @active-count="(j)=>{activeCount = j}"
      @variations-count="(k)=>{variations = k}"
      @add-message="(l) => {message = l}"
      :active="isActive"
      :selectedComposition="activeCount"
      :selectedVariations="variations"
      :addMessage="message"
  />

</template>
