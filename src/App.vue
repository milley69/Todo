<template>
  <div class="card">
    <h1>{{ titleH }}</h1>
    <div class="form-control">
      <input
          type="text"
          v-model="todo"
          :maxlength="maxInput"
          placeholder="Введите вашу задачу..." />

      <button class="btn" @click="addTodo(id++)" >Добавить</button>

    </div>
    <ul class="list" v-for="(todo, i) in todos" :key="todo.id">

      <li :class="{ done: todo.isCompleted }" @dblclick="removeTodo(i)"> <span>{{ i + 1 }}. {{ todo.text }}</span>
        <input v-model="todo.isCompleted" type="checkbox">

      </li>
    </ul>
    <hr />
    <p class="primary">Всего задач: {{ todos.length }}</p>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {},

  data(){
    return {
      titleH: 'Мой Todo лист',
      todo: '',
      maxInput: 25,
      isDone: false,
      id: 0,
      // todos: [{ "id": 1, "text": "qwe", "isCompleted": false }, { "id": 2, "text": "qwesss", "isCompleted": false }]
      todos: []
    }
  },
  methods: {
    addTodo() {
      this.todos.push ({
        id: this.id,
        text: this.todo,
        isCompleted: this.isDone
      });
      this.todo = '';
    },
    removeTodo(index){
      this.todos.splice(index , 1)
    }
  }
}
</script>

<style>
@import "../styles/theme.css";
@import "../styles/main.css";

</style>
