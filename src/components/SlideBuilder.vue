<script>
  import PanelPositions from "./builder/PanelPositions.vue";
  import PanelCollections from "./builder/PanelCollections.vue";
  import PanelOptions from "./builder/PanelOptions.vue";
  import PanelDrag from "./builder/PanelDrag.vue";
  import Preview from "./builder/Preview.vue";

export default {
  components: {
    PanelPositions,
    PanelCollections,
    PanelOptions,
    PanelDrag,
    Preview
  },
  props: ['selectedComposition', 'selectedCollection'],
  data() {
    return {
      selectedCollection: 'gender',
      searchQuery: '',
      filters: ['gender', 'skin', 'outfit', 'hair', 'facial', 'hands', 'glasses'],
      facet: [],
      filterOpen: false,
      panelHeight: '300px',
      collectionItemsCount: false,
      collectionMaxWidth: '100%',
      collectionMaxHeight: '100%',
      collectionClass: false
    }
  }
}
</script>

<template>
  <div class="builder">

    <Preview />

    <div class="builder__panel" :style="{maxHeight: panelHeight}">

      <div class="panel__header">
        <PanelDrag
            @panel-height="(i)=>{panelHeight = i}"
            @collection-max-width="(i)=>{collectionMaxWidth = i}"
            @collection-max-height="(i)=>{collectionMaxHeight = i}"
            @collection-class="(i)=>{collectionClass = i}"
            :collectionItemsCount="collectionItemsCount" />

        <div class="panel__filters filters">
          <form id="search" class="filters__search">
            <input name="query" v-model="searchQuery" class="filters__input" placeholder="Search by category or name">
          </form>
          <div class="filters__selection">
            <button class="filters__button" @click="this.filterOpen = !this.filterOpen">filter</button>
            <div class="filters__selection-inner" :class="{'js-active': this.filterOpen}">
              <ul class="filters__categories">
                <li v-for="item in filters" class="filters__category">
                  <label><input :id="item" type="checkbox" name="facet" v-model="facet" :value="item" checked>{{ item }}</label>
                </li>
              </ul>
            </div>
          </div>
        </div>

        <PanelOptions
            :count="selectedComposition"
            :collection="selectedCollection"
            :filter-key="searchQuery"
            :facet="facet"
            :collectionMaxHeight="collectionMaxHeight"
            :collectionMaxWidth="collectionMaxWidth"
            :collectionClass="collectionClass"
            @collection-items-count="(i)=>{collectionItemsCount = i}"
        />
      </div>

      <div class="panel__footer">
        <PanelCollections @selected-collection="(i) => {selectedCollection = i}"/>
        <PanelPositions :count="selectedComposition" />
      </div>

    </div>
    <div class="builder__modal"></div>
  </div>
</template>

<style scoped>
  .builder {
    height: calc(100vh - 160px);
  }

  .builder__panel {
    position: fixed;
    left: 0;
    bottom: 0;
    height: 100%;
    width: 100%;
    padding-top: 25px;
    background-color: #fff;
    border-radius: 20px 20px 0 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    box-shadow: 0 0 60px 20px rgba(0, 0, 0, 0.1);
  }

  .panel__header {
    height: 100%;
  }

  .panel__filters {
    display: grid;
    grid-template-columns: 1fr 60px;
    grid-gap: 15px;
    margin: 12px 15px;
  }

  .filters__selection {
    position: static;
  }

  .filters__selection-inner {
    position: absolute;
    top: 60px;
    left: 0;
    display: none;
    width: 100%;
    padding: 15px;
    background-color: #fff;
    z-index: 5;
    box-shadow: 0 5px 11px rgba(0, 0, 0, 0.1);
  }

  .filters__selection-inner.js-active {
    display: block;
  }

  .filters__categories {
    padding: 0;
    list-style: none;
    text-align: left;
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .filters__input {
    width: 100%;
    padding: 14px 16px;
    background: #EBEBEB;
    border-radius: 4px;
    font-family: 'Roboto';
    font-size: 12px;
    line-height: 12px;
    letter-spacing: 0.04em;
    color: #000;
    border: none;
  }

  .filters__input::placeholder {
    color: #ABABAB;
  }

  .filters__button {
    font-family: 'Roboto';
    font-size: 11px;
    line-height: 12px;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    border: none;
    background-color: transparent;
  }

  .filters__category {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 6px 10px;
    border: 1px solid #DBDBDB;
    border-radius: 4px;
    font-family: 'Roboto';
    font-size: 11px;
    line-height: 12px;
    letter-spacing: 0.04em;
    text-transform: uppercase;
  }

  .filters__category input {
    /*width: 1px;*/
    /*opacity: 0;*/
  }
</style>
