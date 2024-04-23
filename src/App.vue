<script >
// import Cards from './components/Cards.vue'
export default {
  name: 'app',
  // components: {Cards},
  data () {
    return {
      tasks: [
        {
          "id": 1,
          "title": "Design the website layout for an online store",
          "description": "Create a visually appealing and user-friendly website layout for an online store. Include",
          "category": "to-do"
        },
        {
          "id": 2,
          "title": "Develop the front-end of the website",
          "description": "Implement the front-end of the website using HTML, CSS, and JavaScript. Make sure it is",
          "category": "to-do"
        },
        {
          "id": 3,
          "title": "Design the database schema for the online store",
          "description": "Create a database schema that includes tables for products, customers, orders, and payments",
          "category": "to-do"
        },
        {
          "id": 4,
          "title": "Develop the back-end of the website",
          "description": "Implement the back-end of the website using a server-side language such as Python or Node.js",
          "category": "to-do"
        },
        {
          "id": 5,
          "title": "Implement user authentication and authorization",
          "description": "Create an authentication and authorization system that ensures only authorized users can",
          "category": "to-do"
        },
        {
          "id": 6,
          "title": "Develop the functionality to add, edit, and remove products from the online store",
          "description": "Implement the functionality to add, edit, and remove products from the online store. Also make",
          "category": "to-do"
        },
        {
          "id": 7,
          "title": "Implement a payment gateway for the online store",
          "description": "Create a payment gateway that handles different types of payments and refunds.",
          "category": "to-do"
        },
        {
          "id": 8,
          "title": "Develop the functionality to manage orders and customer information",
          "description": "Implement the functionality to manage orders and customer information. Ensure that each order",
          "category": "to-do"
        },
        {
          "id": 9,
          "title": "Implement a loyalty program for the online store",
          "description": "Create a loyalty program that tracks customer rewards and points.",
          "category": "to-do"
        },
        {
          "id": 10,
          "title": "Develop the functionality to handle product returns and exchanges",
          "description": "Implement the functionality to handle product returns and exchanges. Also make sure it can",
          "category": "to-do"
        },
        {
          "id": 11,
          "title": "Implement a customer service chatbot for the online store",
          "description": "Create a customer service chatbot that handles common questions and provides helpful",
          "category": "to-do"
        },
        {
          "id": 12,
          "title": "Develop the functionality to handle product recommendations and suggestions",
          "description": "Implement the functionality to provide related products and suggestions based on customer",
          "category": "to-do"
        },
        {
          "id": 13,
          "title": "Implement a wishlist feature for the online store",
          "description": "Create a wishlist feature that tracks customer wishlists and products they are interested",
          "category": "to-do"
        },
        {
          "id": 14,
          "title": "Develop the functionality to handle product bundles and discounts",
          "description": "Implement the functionality to provide discounts and promotions to customers.",
          "category": "bug"
        },
        {
          "id": 15,
          "title": "Implement a coupon feature for the online store",
          "description": "Create a coupon feature that tracks customer coupons and rewards.",
          "category": "to-do"
        },
        {
          "id": 16,
          "title": "Develop the functionality to handle product reviews and ratings",
          "description": "Implement the functionality to track product reviews and ratings. Also make sure it can handle",
          "category": "to-do"
        }
      ],
      draggedItem: null
    }
  },
  methods: {
    // async getAllCards () {
    //   await fetch('https://jsonplaceholder.typicode.com/comments?_start=0&_limit=20')
    //       .then(res => res.json())
    //       .then(data => {
    //         this.cards = data; // Assign the fetched data to cards
    //         console.log(this.cards); // Log the fetched data
    //       })
    //       .catch(error => {
    //         console.error('Error fetching data:', error);
    //       });
    //   }
    handleDragStart(index) {
      this.draggedItem = index;
    },
    handleDragOver(event) {
      event.preventDefault();
    },
    handleDrop(category) {
      const droppedTask = this.tasks.splice(this.draggedItem, 1)[0];
      droppedTask.category = category;
      const insertIndex = this.tasks.findIndex(task => task.category === category);
      console.log(insertIndex)
      this.tasks.splice(insertIndex, 0, droppedTask);
      this.draggedItem = null;
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
  <div class="columns" draggable="true" >
      <div class="child to-do"  @dragover.prevent @drop="handleDrop('to-do')">
        <h5>To-do</h5>
<!--        <Cards :cards="this.tasks" />-->
        <div v-for="(item, index) in this.tasks.filter(task => task.category === 'to-do')"
             :key="index"
             class="cards"
             draggable="true"
             @dragstart="handleDragStart(index)"
             @dragend="handleDragEnd"
        >
          <p>{{item}}</p>
      </div>
      </div>
      <div class="child progress"  @dragover.prevent @drop="handleDrop('progress')">
        <div v-for="(item, index) in this.tasks.filter(task => task.category === 'progress')"
             :key="index"
             class="cards"
             draggable="true"
             @dragstart="handleDragStart(index)"
             @dragend="handleDragEnd"
        >
          <p>{{item}}</p>
        </div>
        </div>
      <div class="child done"  @dragover.prevent @drop="handleDrop('done')">
        <div v-for="(item, index) in this.tasks.filter(task => task.category === 'done')"
             :key="index"
             class="cards"
             draggable="true"
             @dragstart="this.handleDragStart(index)"
             @dragover="this.handleDragOver"
             @drop="this.handleDrop(index)"
             @dragend="this.handleDragEnd"
        >
          <p>{{item}}</p>
        </div>
      </div>
      <div class="child bug"  @dragover.prevent @drop="handleDrop('bug')">
        <div v-for="(item, index) in this.tasks.filter(task => task.category === 'bug')"
             :key="index"
             class="cards"
             draggable="true"
             @dragstart="this.handleDragStart(index)"
             @dragover="this.handleDragOver"
             @drop="this.handleDrop(index)"
             @dragend="this.handleDragEnd"
        >
          <p>{{item}}</p>
        </div>
      </div>
  </div>

</template>

<style scoped>
.columns {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100vh;
  margin: 0px 20px;
  /*overflow: hidden;*/
}
.columns .child {
  height: 95vh;
  border: 2px solid #31363F;
  width: 23%;
  overflow: scroll;
}
::-webkit-scrollbar {
  width: 5px;
}
/* Track */
::-webkit-scrollbar-track {
   border-radius: 10px;
}
/* Handle */
::-webkit-scrollbar-thumb {
  background: #4e4e4e;
   border-radius: 5px 0 0 5px;
}
.cards {
  width: 90%;
  margin: 10px;
  font-size: 15px;
  border: 2px solid #31363F;
  border-radius: 5px;
  cursor: pointer;
}
</style>
