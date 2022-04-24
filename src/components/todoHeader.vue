<template>

  <header class="header">
    <h1>Todo Liste</h1>
    <input v-on:keyup.enter="addTodo(newTodo)" v-model="newTodo" type="text" class="new-todo" placeholder="Ajouter une Todo">
  </header>

</template>

<script>
export default {
  name: 'todoHeader',
  props: ['todos'],
  data () {
    return {
      newTodo: ''
    }
  },
  methods: {
    addTodo (todo) {
      // eslint-disable-next-line vue/no-mutating-props
      this.todos.push(todo)
      this.newTodo = ''
    }
  }
}
</script>

<style scoped>

</style>
