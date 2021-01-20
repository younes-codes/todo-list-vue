<template>
  <div class="todos-container">
    <h1>TODOS</h1>
    <form @click.prevent>
      <input type="text" v-model="newTodos" placeholder="Ajouter un tâche" />
      <input class="add" type="submit" value="Ajouter" @click="addToDo" />
    </form>
    <input type="checkbox" v-model="allDone" />
    <ul>
      <li v-for="(todo, index) in filteredTodos" :key="index">
        <label class="container">
          <input type="checkbox" v-model="todo.completed" />
          <span class="checkmark"></span>
        </label>
        <p :class="{ todoCompleted: todo.completed }">
          {{ todo.name }}
        </p>
        <button class="delete" @click="deleteToDo(index)">X</button>
      </li>
    </ul>
    <footer>
      <span class="todo-count" v-show="todos.length > 0">
        <strong>{{ remaining }}</strong>
        Tâches à faire
      </span>
      <ul class="filters">
        <li
          :class="{ selected: filter === 'all' }"
          @click.prevent="filter = 'all'"
        >
          <a href="">Toutes les tâches</a>
        </li>
        <li
          :class="{ selected: filter === 'todo' }"
          @click.prevent="filter = 'todo'"
        >
          <a href="">A faire</a>
        </li>
        <li
          :class="{ selected: filter === 'done' }"
          @click.prevent="filter = 'done'"
        >
          <a href="">Faites</a>
        </li>
      </ul>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodos: "",
      filter: "all",
    };
  },
  methods: {
    addToDo() {
      if (this.newTodos !== "") {
        this.todos.push({
          name: this.newTodos,
          completed: false,
        });
        this.newTodos = "";
      } else {
        return false;
      }
    },
    deleteToDo(todo) {
      this.todos.splice(todo, 1);
    },
  },
  computed: {
    remaining() {
      return this.todos.filter((todo) => !todo.completed).length;
    },
    allDone: {
      get() {
        return this.remaining === 0;
      },
      set(value) {
        this.todos.forEach((todo) => {
          todo.completed = value;
        });
      },
    },
    filteredTodos() {
      if (this.filter === "todo") {
        return this.todos.filter((todo) => !todo.completed);
      } else if (this.filter === "done") {
        return this.todos.filter((todo) => todo.completed);
      }
      return this.todos;
    },
  },
};
</script>

<style lang="scss">
form {
  display: flex;
  justify-content: space-between;
  width: 350px;
  margin: 20px auto 20px;
  input[type="text"] {
    width: 90%;
    max-width: 300px;
    margin-right: 10px;
  }
}
ul {
  width: 350px;
  margin: auto;
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 1.5rem;
    margin-bottom: 10px;

    .delete {
      text-decoration: none;
    }
  }
}

.filters {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
  li {
    a {
      text-decoration: none;
      color: #cccccc;
    }
  }
  .selected {
    border: 1px solid #726e6e;
    border-radius: 5px;
    padding: 5px;
  }
}

.todo-count {
  font-size: 1.5rem;
}

.todoCompleted {
  color: #726e6e;
  text-decoration: line-through;
}

.add {
  background-color: rgb(4, 105, 105);
  border: 0;
  padding: 10px;
  width: 100px;
}

.delete {
  background-color: rgb(219, 127, 127);
  width: 20px;
  height: 20px;
  padding: 10px;
  border: 0;
}

/* Customize the label (the container) */
.container {
  display: block;
  position: relative;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: -10px;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: #eee;
  border: 1px solid #cccccc;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #f4f4f4;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #1fc572;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
