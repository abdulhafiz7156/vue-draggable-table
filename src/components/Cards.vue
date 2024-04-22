<script>

export default {
  name: "Cards-List",
  data() {
    return {
      draggedItem: null
    }
  },

  props: ['cards'],
  methods: {
    handleDragStart(index) {
      this.draggedItem = index;
      console.log(this.draggedItem);
    },
    handleDragOver(event) {
      event.preventDefault();
    },
    handleDrop(index) {
      const droppedItem = this.cards.splice(this.draggedItem, 1)
      console.log(droppedItem[0]);
      this.cards.splice(index, 0, droppedItem[0])
      this.draggedItem = null
    },
    handleDragEnd() {
      this.draggedItem = null;
    }
  },
  created() {
  }

}
</script>

<template>
  <div v-for="(item, index) in this.cards"
       :key="index"
       class="cards"
       draggable="true"
       @dragstart="this.handleDragStart(index)"
       @dragover="this.handleDragOver"
       @drop="this.handleDrop(item.id)"
       @dragend="this.handleDragEnd"
       >
    <p>{{item}}</p>
  </div>
</template>

<style scoped>
.cards {
  width: 90%;
  margin: 10px;
  font-size: 15px;
  border: 2px solid #31363F;
  border-radius: 5px;
  cursor: pointer;
}
</style>
