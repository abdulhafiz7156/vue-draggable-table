<script >
import Cards from './components/Cards.vue'
export default {
  name: 'app',
  components: {Cards},
  data () {
    return {
      cards: [],
    }
  },
  methods: {
    async getAllCards () {
      await fetch('https://jsonplaceholder.typicode.com/comments?_start=0&_limit=20')
          .then(res => res.json())
          .then(data => {
            this.cards = data; // Assign the fetched data to cards
            console.log(this.cards); // Log the fetched data
          })
          .catch(error => {
            console.error('Error fetching data:', error);
          });
      }
  },
  created() {
    this.getAllCards()
  }

}
</script>

<template>
  <div class="columns">
    <div class="to-do">
      <Cards :cards="this.cards" />
    </div>
    <div class="progress"></div>
    <div class="done"></div>
    <div class="bug"></div>
  </div>
</template>

<style scoped>
.columns {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100vh;
}
.columns div {
  /*height: 95vh;*/
  border: 2px solid white;
  width: 20%;
}
</style>
