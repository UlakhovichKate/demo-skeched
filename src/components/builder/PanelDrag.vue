<script>

export default {
  emits: ['panel-height', 'collection-max-height', 'collection-max-width', 'collection-class'],
  props: ['collectionItemsCount'],
  data() {
    return {
      isDragging: false,
      start: { x: 0, y: 0 },
      headerHeight: 120,
      c: { x: 0, y: 0 },
      panelHeight: 0,
      collectionMaxHeight: '100%',
      collectionMaxWidth: '100%',
    }
  },
  methods: {
    dragStart(e) {
      e = e.changedTouches ? e.changedTouches[0] : e
      this.isDragging = true
      this.start.x = e.pageX
      this.start.y = e.pageY
    },
    dragEnter(e) {
      e = e.changedTouches ? e.changedTouches[0] : e
      if (this.isDragging) {
        this.c.y = this.headerHeight + (e.pageY - this.start.y)
        this.panelHeight = (window.innerHeight - e.pageY) + "px"
        this.$emit('panel-height', this.panelHeight);
        this.countWidth(e);
      }
    },
    dragEnd() {
      if (this.isDragging) {
        this.isDragging = false
      }
    },
    countWidth (e) {
      let itemWidth = 104; // default
      let rowsCount = Math.floor(((window.innerHeight - e.pageY) / 3) / Number(itemWidth));
      let columnsCount = Math.ceil(this.collectionItemsCount / Number(rowsCount > 0 ? rowsCount : 1));
      let elmnt = document.querySelector('.builder__panel');

      if (((window.innerHeight - e.pageY) / 2) > 200) {
        this.collectionMaxHeight = (window.innerHeight - e.pageY) / 2  + "px";

        if ((columnsCount * itemWidth) > elmnt.offsetWidth) {
          this.collectionMaxWidth = columnsCount * itemWidth + "px";
        }
        this.$emit('collection-class', false);

      } else {
        this.collectionMaxHeight = '100%';
        this.collectionMaxWidth = '100%';
        this.$emit('collection-class', true);
      }

      this.$emit('collection-max-height', (this.collectionMaxHeight))
      this.$emit('collection-max-width', (this.collectionMaxWidth))
    }
  }
}
</script>

<template>
  <div class="panel__drag drag" draggable="true"
       @mousedown="dragStart"
       @touchstart="dragStart"
       @mousemove="dragEnter"
       @touchmove="dragEnter"
       @mouseup="dragEnd"
       @touchend="dragEnd"
       @mouseleave="dragEnd"
  ></div>

</template>

<style scoped>
  .drag {
    position: absolute;
    top: -23px;
    width: 100%;
    height: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .drag::after {
    content: '';
    display: block;
    width: 45px;
    height: 4px;
    background-color: #DBDBDB;
  }
</style>
