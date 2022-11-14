<template>
  <div class="card">
    <h1>{{ titleH }}</h1>
    <div class="form-control">
      <input
          type="text"
          v-model="todo"
          :maxlength="maxInput"
          @keypress.enter="addTodo(id++)"
          placeholder="Введите вашу задачу..." />

      <button class="btn" @click="addTodo(id++)" >Добавить</button>

    </div>
    <ul class="list" v-for="(todo, i) in todos" :key="todo.id">

      <li :class="{ done: todo.isCompleted }" @dblclick="removeTodo(i)">
        <span title="Двойной клик для удаления" >{{ i + 1 }}. {{ todo.text }}</span>
        <input v-model="todo.isCompleted" @change="checkLS()" type="checkbox">

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

  async mounted(){
    const data = await localStorage.getItem('todos')
    if (data){
      this.todos = JSON.parse(data)
    }
  },


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
      if (this.todo !== ""){
        this.todos.push ({
          id: this.id,
          text: this.todo,
          isCompleted: this.isDone
        })
      }
      localStorage.setItem('todos', JSON.stringify(this.todos))
      this.todo = '';
    },
    removeTodo(index){
      this.todos.splice(index , 1)
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    checkLS(){
      console.log(this.isDone)
      localStorage.setItem('todos', JSON.stringify(this.todos))
    }
  }
}
</script>

<style>
@import "../styles/theme.css";
@import "../styles/main.css";

</style>