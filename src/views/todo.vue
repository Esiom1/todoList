<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todo Liste</h1>
      <input v-on:keyup.enter="addTodo(newTodo)" v-model="newTodo" type="text" class="new-todo" placeholder="Ajouter une Todo">
    </header>
    <div class="main">
      <ul class="todo-list">
        <li v-bind:class="{completed: todo.state, editing:todo===editing}" v-for="(todo, index) in filteredTodo" v-bind:key="index" class="todo ">
          <div class="view">
            <input v-on:click="updateState" v-model="todo.state" type="checkbox" name="" id="" class="toggle">
            <label v-on:dblclick="editeTodo(todo)">{{todo.name}}</label>
            <button v-on:click.prevent="deleteTodo(index)" class="destroy"></button>
          </div>
          <input v-on:keypress.enter="saveTodoEdited()" type="text" class="edit" v-model="todo.name">
        </li>
      </ul>
    </div>
    <footer v-show="hasTodo" class="footer">
      <span class="todo-count"><strong>{{nbTodoRestant}}</strong> tache<span v-if="nbTodoRestant > 1">s</span>  à faire</span>
      <ul class="filters">
        <li><a href="#" v-bind:class="{selected: filter==='all' }" v-on:click.prevent="filter = 'all' ">Toutes</a></li>
        <li><a href="#" v-bind:class="{selected: filter==='todo' }" v-on:click.prevent="filter = 'todo'">A faire</a></li>
        <li><a href="#" v-bind:class="{selected: filter==='done' }" v-on:click.prevent="filter = 'done'">Faites</a></li>
      </ul>
    </footer>
  </section>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'todo',
  data () {
    return {
      todos: [],
      newTodo: '',
      filter: 'all',
      editing: null
    }
  },
  methods: {
    addTodo (todo) {
      // eslint-disable-next-line vue/no-mutating-props
      this.todos.push({ name: this.newTodo, state: false })
      this.newTodo = ''
    },
    updateState () {
      this.todos.state = !this.todos.state
    },
    deleteTodo (key) {
      this.todos.splice(key, 1)
    },
    editeTodo (todo) {
      this.editing = todo
    },
    saveTodoEdited () {
      this.editing = null
    }
  },
  computed: {
    // eslint-disable-next-line vue/return-in-computed-property
    nbTodoRestant () {
      const todoRestant = this.todos.filter(function (todo) {
        return !todo.state
      })
      return todoRestant.length
    },
    filteredTodo () {
      if (this.filter === 'todo') {
        return this.todos.filter(function (todo) {
          return !todo.state
        })
      } else if (this.filter === 'done') {
        return this.todos.filter(function (todo) {
          return todo.state
        })
      }
      return this.todos
    },
    hasTodo () {
      return this.todos.length > 0
    }
  },
  mounted () {
    console.log(this.todos)
  }

}
</script>

<style   scoped>

</style>
