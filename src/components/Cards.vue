<script>

export default {
  name: "Cards-List",
  data() {
    return {
    }
  },

  props: ['cards'],
  methods: {

  },
  created() {
  }

}
</script>

<template>
  <div v-for="(items, index) in this.cards" :key="index" class="cards">
    <p>{{items.body}}</p>
  </div>
</template>

<style scoped>
.cards {
  width: 90%;
  font-size: 15px;
  border: 2px solid white;
}
</style>
