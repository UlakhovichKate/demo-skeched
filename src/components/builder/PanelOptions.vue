<script>
export default {
  props: ['collection', 'count', 'filterKey', 'facet', 'collectionMaxHeight', 'collectionMaxWidth', 'collectionClass'],
  emits: ['collection-items-count'],
  data() {
    return {
      current: false,
      layers: [
        {name: 'gender', title: 'Gender'},
        {name: 'skin', title: 'Skin Tone'},
        {name: 'outfit', title: 'Outfit'},
        {name: 'hair', title: 'Hair'},
        {name: 'facial', title: 'Facial Hair'},
        {name: 'hands', title: 'Hands Props'},
        {name: 'glasses', title: 'Glasses'},
      ],
      searchQuery: null,
    }
  },
  methods: {
    createImageUrl(el) {
      return "/assets/layers/" + el + ".png"
    },
    setActivePosition(i) {
      this.current = i;
    }
  },
  computed: {
    filterPosts(){
      return this.layers.filter(result => {
        const myRegex = new RegExp(this.filterKey, 'gi');
        let resultFacet = this.facet;
        if (resultFacet.length === 0) {
          return (result.title.match(myRegex) || result.name.match(myRegex))
        }
        return (result.title.match(myRegex) || result.name.match(myRegex)) && (resultFacet.includes(result.name));
      })
    }
  },
  mounted() {
    this.$emit('collection-items-count', this.layers.length);
  }
}
</script>

<template>
  <div class="panel__options">
    <div class="options" :data-collection="collection.name" :data-count="count.name" :data-itemsCount="layers.length"  :style="{'maxHeight': collectionMaxHeight, 'width': collectionMaxWidth}" :class="{'nowrap': collectionClass}">
      <button v-for="(option, index) in filterPosts" type="button" class="options__button" :class="{'js-active' : index === current}" :data-collection="collection.name" @click="setActivePosition(index)">
        <img :alt="option.title" :src="createImageUrl(option.name)" class="options__img">
      </button>
    </div>
  </div>
</template>

<style scoped>
  .panel__options {
    overflow-x: scroll;
  }

  .options {
    display: flex;
    flex-wrap: wrap;
    gap: 7px;
    padding: 6px 15px 6px;
    overflow: hidden;
  }

  .options.nowrap {
    flex-wrap: nowrap;
    overflow-x: scroll;
  }

  .options__button {
    min-width: 104px;
    width: 104px;
    height: 104px;
    background: transparent;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border: 1px solid #DBDBDB;
    border-radius: 4px;
  }

  .options__button.js-active {
    border-color:  #FFBD9B;
  }

  .options__button:hover {
    border-color:  #FFBD9B;
  }

</style>
