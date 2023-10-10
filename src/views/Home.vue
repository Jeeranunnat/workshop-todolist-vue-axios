<template>
  <div class="home">
    <div class="container">
      <TodoAdd @onSubmit="addTask" />
      <!--  <TodoList :tasks="reverseTasks" @onRemove="removeTask" @onToggle="toggleTask" /> -->
      <TodoList :tasks="reverseTasks" @onRemove="removeTask" @onToggle="toggleTask" />
    </div>
  </div>
</template>

<script>
import TodoList from "../components/TodoList.vue";
import TodoAdd from "../components/TodoAdd.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    TodoList,
    TodoAdd,
  },
  computed: {
    reverseTasks() {
      return this.tasks.slice().reverse();
    }
  },
  async mounted() {
    let result = await axios.get("https://jsonplaceholder.typicode.com/todos");
    this.tasks = result.data.map((task) => {
      return {
        id: task.id,
        name: task.title,
        complete: task.completed,
      };
    });
  },
  data() {
    return {
      tasks: [],
      tasks_mockup: [
        {
          id: 1,
          name: "Task1",
          complete: false,
        },
        {
          id: 2,
          name: "Task2",
          complete: false,
        },
        {
          id: 3,
          name: "Task3",
          complete: false,
        },
      ],
    };
  },
  methods: {
    async addTask(item) {
      let modifyItem = {
        id: item.id,
        title: item.name,
        completed: item.complete,
      };
      let result = await axios.post("https://jsonplaceholder.typicode.com/todos", modifyItem);
      console.log(JSON.stringify(result.data));
      // this.tasks.push(result.data);
      this.tasks.push(item);
    },
    removeTask(id) {
      axios.delete("https://jsonplaceholder.typicode.com/todos/" + id).then(result => {
        console.log(JSON.stringify(result.data))
        this.tasks = this.tasks.filter((item) => item.id !== id);
      }).catch(error => {
        console.log(error)
      })
    },
    toggleTask(id) {
      this.tasks.forEach((item) => {
        if (item.id === id) {
          item.complete = !item.complete;
          //console.log(this.tasks);
        }
      });
    },
  },
};
</script>
<style>
.home {
  display: flex;
  justify-content: space-around;
}

.container {
  width: 60vw;
}
</style>
