<script>
export default {
  emits: ['selected-collection'],
  data() {
    return {
      currentPosition: 1,
      collections: [
        {name: 'gender', title: 'Gender'},
        {name: 'skin', title: 'Skin Tone'},
        {name: 'outfit', title: 'Outfit'},
        {name: 'hair', title: 'Hair'},
        {name: 'facial', title: 'Facial Hair'},
        {name: 'hands', title: 'Hands Props'},
        {name: 'glasses', title: 'Glasses'},
      ]
    }
  },
  methods: {
    createImageUrl(el) {
      return "/assets/svg/" + el + ".svg"
    },
    setActivePosition(i) {
      this.currentPosition = i;
      this.$emit('selected-collection', this.collections[this.currentPosition]);
    }
  }
}
</script>

<template>
  <div class="panel__collections collections">
    <button v-for="(collection, index) in collections" type="button" class="collections__button" :class="{'js-active' : index === currentPosition}" :data-collection="collection" @click="setActivePosition(index)">
      <img :alt="collection.title" :src="createImageUrl(collection.name)" class="collections__svg">
      <span class="collections__name">{{ collection.title }}</span>
    </button>
  </div>
</template>

<style scoped>
  .collections {
    display: flex;
    flex-wrap: nowrap;
    gap: 7px;
    padding: 6px 15px 9px;
    overflow-x: scroll;
  }

  .collections__button {
    min-width: 75px;
    width: 75px;
    height: 75px;
    background: transparent;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border: 1px solid transparent;
    border-radius: 4px;
  }

  .collections__button.js-active {
    background-color: #FFBD9B;
    border-color:  #FFBD9B;
  }

  .collections__button:hover {
    border-color:  #FFBD9B;
  }

  .collections__name {
    margin-top: 7px;
    font-family: 'Roboto';
    font-size: 11px;
    line-height: 12px;
    text-align: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    color: #999999;
  }

  .collections__button.js-active .collections__name,
  .collections__button:hover .collections__name{
    color: #000;
  }
</style>
