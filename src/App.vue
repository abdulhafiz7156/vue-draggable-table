<script >
import Cards from './components/Cards.vue'
export default {
  name: 'app',
  components: {Cards},
  data () {
    return {
      cards: [],
      tasks:[
        {
          "id": 1,
          "title": "Design the website layout for an online store",
          "description": "Create a visually appealing and user-friendly website layout for an online store. Include"
        },
        {
          "id": 2,
          "title": "Develop the front-end of the website",
          "description": "Implement the front-end of the website using HTML, CSS, and JavaScript. Make sure it is"
        },
        {
          "id": 3,
          "title": "Design the database schema for the online store",
          "description": "Create a database schema that includes tables for products, customers, orders, and payments"
        },
        {
          "id": 4,
          "title": "Develop the back-end of the website",
          "description": "Implement the back-end of the website using a server-side language such as Python or Node.js"
        },
        {
          "id": 5,
          "title": "Implement user authentication and authorization",
          "description": "Create an authentication and authorization system that ensures only authorized users can"
        },
        {
          "id": 6,
          "title": "Develop the functionality to add, edit, and remove products from the online store",
          "description": "Implement the functionality to add, edit, and remove products from the online store. Also make"
        },
        {
          "id": 7,
          "title": "Implement a payment gateway for the online store",
          "description": "Create a payment gateway that handles different types of payments and refunds.",
        },
        {
          "id": 8,
          "title": "Develop the functionality to manage orders and customer information",
          "description": "Implement the functionality to manage orders and customer information. Ensure that each order"
        },
        {
          "id": 9,
          "title": "Implement a loyalty program for the online store",
          "description": "Create a loyalty program that tracks customer rewards and points.",
        },
        {
          "id": 10,
          "title": "Develop the functionality to handle product returns and exchanges",
          "description": "Implement the functionality to handle product returns and exchanges. Also make sure it can"
        },
        {
          "id": 11,
          "title": "Implement a customer service chatbot for the online store",
          "description": "Create a customer service chatbot that handles common questions and provides helpful"
        },
        {
          "id": 12,
          "title": "Develop the functionality to handle product recommendations and suggestions",
          "description": "Implement the functionality to provide related products and suggestions based on customer"
        },
        {
          "id": 13,
          "title": "Implement a wishlist feature for the online store",
          "description": "Create a wishlist feature that tracks customer wishlists and products they are interested"
        },
        {
          "id": 14,
          "title": "Develop the functionality to handle product bundles and discounts",
          "description": "Implement the functionality to provide discounts and promotions to customers.",
        },
        {
          "id": 15,
          "title": "Implement a coupon feature for the online store",
          "description": "Create a coupon feature that tracks customer coupons and rewards.",
        },
        {
          "id": 16,
          "title": "Develop the functionality to handle product reviews and ratings",
          "description": "Implement the functionality to track product reviews and ratings. Also make sure it can handle"
        }
      ],
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
  },
  created() {
  }

}
</script>

<template>
  <div class="columns" >
      <div class="to-do">
        <h5>To-do</h5>
        <Cards :cards="this.tasks" />
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
  margin: 0px 20px;
  /*overflow: hidden;*/
}
.columns div {
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
</style>
