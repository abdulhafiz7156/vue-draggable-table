<script>
// import Cards from './components/Cards.vue'
export default {
  name: 'app',
  // components: {Cards},
  data() {
    return {
      tasks: [
        {
          "id": 1,
          "title": "Design the website layout for an online store",
          "description": "Create a visually appealing and user-friendly website layout for an online store. Include",
          "category": "to-do",
          "status": "pending",
          "date": "12-04-2024"
        },
        {
          "id": 2,
          "title": "Develop the front-end of the website",
          "description": "Implement the front-end of the website using HTML, CSS, and JavaScript. Make sure it is",
          "category": "to-do",
          "status": "pending",
          "date": "9-04-2024"
        },
        {
          "id": 3,
          "title": "Design the database schema for the online store",
          "description": "Create a database schema that includes tables for products, customers, orders, and payments",
          "category": "to-do",
          "status": "pending",
          "date": "8-04-2024"
        },
        {
          "id": 4,
          "title": "Develop the back-end of the website",
          "description": "Implement the back-end of the website using a server-side language such as Python or Node.js",
          "category": "to-do",
          "status": "pending",
          "date": "12-04-2024"
        },
        {
          "id": 5,
          "title": "Implement user authentication and authorization",
          "description": "Create an authentication and authorization system that ensures only authorized users can",
          "category": "to-do",
          "status": "pending",
          "date": "1-04-2024"
        },
        {
          "id": 6,
          "title": "Develop the functionality to add, edit, and remove products from the online store",
          "description": "Implement the functionality to add, edit, and remove products from the online store. Also make",
          "category": "to-do",
          "status": "pending",
          "date": "24-04-2024"
        },
        {
          "id": 7,
          "title": "Implement a payment gateway for the online store",
          "description": "Create a payment gateway that handles different types of payments and refunds.",
          "category": "to-do",
          "status": "pending",
          "date": "12-04-2024"
        },
        {
          "id": 8,
          "title": "Develop the functionality to manage orders and customer information",
          "description": "Implement the functionality to manage orders and customer information. Ensure that each order",
          "category": "to-do",
          "status": "pending",
          "date": "12-04-2024"
        },
        {
          "id": 9,
          "title": "Implement a loyalty program for the online store",
          "description": "Create a loyalty program that tracks customer rewards and points.",
          "category": "to-do",
          "status": "pending",
          "date": "12-04-2024"
        },
        {
          "id": 10,
          "title": "Develop the functionality to handle product returns and exchanges",
          "description": "Implement the functionality to handle product returns and exchanges. Also make sure it can",
          "category": "progress",
          "status": "pending",
          "date": "12-04-2024"
        },
        {
          "id": 11,
          "title": "Implement a customer service chatbot for the online store",
          "description": "Create a customer service chatbot that handles common questions and provides helpful",
          "category": "done",
          "status": "pending",
          "date": "12-04-2024"
        },
        {
          "id": 12,
          "title": "Develop the functionality to handle product recommendations and suggestions",
          "description": "Implement the functionality to provide related products and suggestions based on customer",
          "category": "bug",
          "status": "pending",
          "date": "12-04-2024"
        }
      ],
      columns: [
        {
          id: 1,
          name: 'To-Do',
          class: 'to-do'
        },
        {
          id: 2,
          name: 'Progress',
          class: 'progress'
        },
        {
          id: 3,
          name: 'Done',
          class: 'done'
        },
        {
          id: 4,
          name: 'Bug',
          class: 'bug'
        },
      ],
      draggedItem: null,
      showPopup: false,
      username: '',
      repository: '',
      branches: null,
      taskPopup: false,
      selectedTaskPopup: null,
      newTask: {
        id: null,
        title: null,
        description: null,
        category: null,
        status: "pending",
        date: null
      },
      createTaskDiv: false,
    }
  },
  methods: {
    handleDragStart(index) {
      console.log(index)
      this.draggedItem = index;
    },
    handleDragOver(event) {
      event.preventDefault();
    },
    handleDrop(category) {
      const droppedTask = this.tasks.find(task => task.id === this.draggedItem);
      droppedTask.category = category;
      if (droppedTask.category === category) {
        return;
      }
      const index = this.tasks.findIndex(task => task.id === this.draggedItem);
      this.tasks.splice(index, 1);
      const insertIndex = this.tasks.findIndex(task => task.category === category);
      if (insertIndex !== -1) {
        this.tasks.splice(insertIndex, 0, droppedTask);
      } else {
        this.tasks.push(droppedTask);
      }
      this.draggedItem = null;
    },
    handleDragEnd() {
      this.draggedItem = null;
    },
    openPopup() {
      this.showPopup = true;
    },
    fetchBranches() {
      fetch(`https://api.github.com/repos/${this.username}/${this.repository}/branches`)
          .then(response => {
            if (!response.ok) {
              throw new Error('Network response was not ok');
            }
            return response.json();
          })
          .then(data => {
            this.branches = data;
            console.log(this.branches);
            localStorage.setItem('githubBranches', JSON.stringify(data));
            this.showPopup = false;
          })
          .catch(error => {
            console.error('Error fetching data:', error);
          });
    },
    filteredTasks(columnName) {
      return this.tasks.filter(task => task.category === columnName)
    },
    openTaskPopup(task) {
      this.taskPopup = true;
      this.selectedTaskPopup = task;
    },
    deleteTask(id) {
      const index = this.tasks.findIndex(task => task.id === id);
      if (index !== -1) {
        this.tasks.splice(index, 1);
      }
      this.taskPopup = false;
    },
    createTask(category) {
      const currentDate = new Date();
      const day = currentDate.getDate();
      const month = currentDate.getMonth() + 1;
      const year = currentDate.getFullYear();
      const lastId = this.tasks.pop().id
      this.newTask.id = lastId + 1;
      this.newTask.date = `${day}-${month}-${year}`;
      this.newTask.category = category;
      this.tasks.push(this.newTask);
      this.createTaskDiv = false
      this.newTask = {
        id: null,
        title: null,
        description: null,
        category: null,
        status: "pending",
        date: null
      }
    },
    openCloseTask() {
      this.createTaskDiv = true;
    }
  },
  created() {
    if (localStorage.getItem('githubBranches')) {
      this.showPopup = false
      this.branches = JSON.parse(localStorage.getItem('githubBranches'));
    } else {
      this.showPopup = true
    }
  }

}
</script>

<template>
  <div class="columns">
    <div
        class="child"
        v-for="(column, index) in this.columns"
        :class="column.class"
        :key="index"
        @dragover.prevent
        @drop="handleDrop(column.class)"
    >
      <div class="container">
        <h5>{{ column.name }} {{ filteredTasks(column.class).length }}</h5>
        <div v-for="(item, index) in filteredTasks(column.class)"
             :key="index"
             class="cards"
             draggable="true"
             @dragstart="handleDragStart(item.id)"
             @dragend="handleDragEnd"
             @click="openTaskPopup(item)"
        >
          <h4>{{ item.title }}</h4>
          <div style="display: flex">
            <p style="margin-right: 20px">{{ item.date }}</p>
            <p>{{ item.status }}</p>
          </div>
        </div>
        <div class="cards create__task">
          <p v-if="!this.createTaskDiv" @click="this.openCloseTask()" >+</p>
          <div v-if="this.createTaskDiv">
            <input type="text" v-model="this.newTask.title">
            <button @click="createTask(column.class)">Save</button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- Popup -->
  <div v-if="this.showPopup" class="popup">
    <div class="popup-content">
      <span class="close" @click="this.showPopup = false">&#10005;</span>
      <h2>To integrate your GitHub repository, please add it below.</h2>
      <div class="input__div">
        <input type="text" v-model="this.username" placeholder="GitHub Username">
        <input type="text" v-model="this.repository" placeholder="Repository Name">
      </div>
      <button @click="this.fetchBranches">Fetch Branches</button>
    </div>
  </div>
  <!-- Task Popup -->
  <div v-if="taskPopup" class="popup task__popup">
    <div class="popup-content task__popup__content">
      <span class="close" @click="this.taskPopup = false" @click.self="this.taskPopup = false">&times;</span>
      <h2>Task Details</h2>
      <div>
        <label for="title">Title:</label>
        <input type="text" id="title" v-model="selectedTaskPopup.title"/>
        <label for="description">Description:</label>
        <textarea id="description" v-model="selectedTaskPopup.description"></textarea>
        <label for="status">Status:</label>
        <select id="status" v-model="selectedTaskPopup.status">
          <option value="pending">Pending</option>
          <option value="in-progress">In Progress</option>
          <option value="completed">Completed</option>
        </select>
        <label for="branches">GitHub Branches:</label>
        <select id="branches" v-model="this.branches.name">
          {{ this.branches }}
          <option v-for="(branch, index) in this.branches" :key="index" :value="branch.name">{{ branch.name }}</option>
        </select>
        <div class="task__popup__button__div">
          <button @click="this.taskPopup = false">Save</button>
          <button @click="this.deleteTask(selectedTaskPopup.id)">Delete</button>
        </div>
      </div>
    </div>
  </div>
</template>

