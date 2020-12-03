<template>
  <div class="wrapper">
    <h1>say "no" to procrastination</h1>
    <div class="newtodo">
      <input
        type="text"
        name="todo-text"
        v-model.trim="newTodoText"
        class="todo-text"
        placeholder="New todo"
      />
      <datepicker v-on:update="dateUpdated"/>
      <button class="todo-add-button" v-on:click="addTodo()">+</button>
    </div>
    
    <ul v-if="todos.length">
      <li class="todo">
        <span class="todo-text list-header">Todo</span>
        <span class="todo-date list-header">Due date</span>
        <span class="todo-empty-button list-header"></span>
      </li>

      <li class="todo" v-for="todo in todos" :key="todo.id">
        <!-- <span class="todo-text">{{ todo.text }}</span>
        <span class="todo-date">{{ todo.date.format('MM-DD-YYYY') }}</span>
        <button class="todo-remove-button" v-on:click="removeTodo(todo)">Remove</button> -->
        <todo :todo="todo" v-on:remove="removeTodo(todo)"/>
      </li>
    </ul>
    <p class="none" v-else>Add a new todo in the input above</p>
  </div>
</template>

<script>
import datepicker from './components/datepicker.vue'
import todo from './components/todo.vue'

export default {
  name: "App",
  components: {
    datepicker,
    todo
  },
  data() {
    return {
      newTodoText: "",
      newTodoDate: "",
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodoText) {

        this.todos.push({
          text: this.newTodoText,
          date: this.newTodoDate,
          id: Date.now(),
          done: false
        });

        this.todos.sort((todoA, todoB) => -todoA.date.diff(todoB.date))

        this.newTodoText = "";
      }
    },
    
    removeTodo (item) {
      this.todos = this.todos.filter((_item) => _item !== item);
    },

    dateUpdated (date) {
      this.newTodoDate = date.clone()
    }
  },
};
</script>

<style>
/* *{
    background-color: #d83ea56b ;

}
html, */
body {
  font: 16px/1.2 BlinkMacSystemFont, -apple-system, "Segoe UI", Roboto,
    Helvetica, Arial, sans-serif;
  padding: 10px;
  background-color: rgb(247, 232, 148);

}
h1{
  font-size: 1em;
  text-align: center;
  background-color: rgb(110, 212, 246);
  text-transform: uppercase;
  padding: 1%;
}
.wrapper {
  width: 75%;
  margin: 0 auto;
}

.newtodo {
  display: flex;
  width: 100%;
}

.todo {
  display: flex;
  width: 100%;
  margin-bottom: 5px;
}

.list-header {
  text-align: center;
  padding: 5px;
  margin-left: 2px;
  margin-right: 2px;
  background-color: #eee;
  color: black;
}

.todo-text {
  flex: 4;
  text-align: center;
}

.todo-date {
  flex: 3;
  text-align: center;
}

.todo-add-button {
  flex: 1;
  border: 1px solid green;
  background: green;
  color: white;
  font-size: 0.8rem;
  padding: 2px 30px;
  cursor: pointer;
  margin-left: 2px;
  margin-right: 2px;
  outline: none;
}

.todo-remove-button {
  flex: 1;
  border: 1px solid red;
  background-color: red;
  color: white;
  font-size: 0.8rem;
  padding: 2px 4px;
  cursor: pointer;
  margin-left: 2px;
  margin-right: 2px;
}

.todo-empty-button {
  flex: 1;
  padding: 2px 4px;
  margin-left: 2px;
  margin-right: 2px;
}

ul, li {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

ul {
    margin-top: 40px;
}

button {
  border: 1px solid green;
  background: green;
  color: white;
  font-size: 0.8rem;
  padding: 2px 4px;
  cursor: pointer;
}

p.none {
  color: #888;
  font-size: small;
}
/* *, *::before, *::after {
  box-sizing: border-box;

}
html, body {
  font: 16px/1.2 BlinkMacSystemFont, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  padding: 10px;
}

.wrapper {
  width: 75%;
  margin: 0 auto;

}

#newtodo {
  width: 100%;
}

input {
  border: 1px solid white;
  width: 85%;
  border-radius: 10px;
  padding: 7px;
  background-image: linear-gradient(319deg, #fceb00 0%, #ef4063 37%, #e557c6 100%);

}

button {
  border: 1px solid green;
  border-radius: 60px;
  background: green;
  color: white;
  font-size: 0.9rem;
  cursor: pointer;
  width: 30px;
  padding: 3px;
  margin-left: 5px;
}
form #todo-text {
  width: 100%;
  padding: 10px;
  border: 1px solid #777;
  
}

ul, li {
  margin: 0;
  padding: 0;
}

p.none {
  color: #888;
  font-size: small;
}

.todo li {
  display: flex;
  margin: 5px 0;
  background-color: white;
  border-radius: 10px;
}
span{
  border-bottom: 1px solid black;
}
.todo li span {
  flex: 1;
}
.todo li button {
  border: 1px solid rgb(198,78,17);
  border-radius: 60px;
  background: rgb(198, 78, 17);
  color: white;
  font-size: 0.9rem;
  cursor: pointer;
  width: 30px;
  padding: 3px;
} */
</style>