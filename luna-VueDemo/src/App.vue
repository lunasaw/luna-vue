<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <TodoHeader :addTodo="addTodo"/>
      <TodoList :todos="todos" :deleteTodo="deleteTodo"/>
      <TodoFooter :todos="todos" :deleteCompleteTodos="deleteCompleteTodos" :selectAllTodos="selectAllTodos"/>
    </div>
  </div>
</template>

<script>
import TodoFooter from './components/TodoFooter'
import TodoHeader from './components/TodoHeader'
import TodoList from './components/TodoList'
export default {
  name: 'App',
  data () {
    return {
      todos: [
        {title: '吃饭', complete: false},
        {title: '睡觉', complete: true},
        {title: 'coding', complete: false}
      ]
    }
  },
  methods: {
    addTodo (todo) {
      this.todos.unshift(todo)
    },
    deleteTodo (index) {
      this.todos.splice(index, 1)
    },
    deleteCompleteTodos () {
      // 删除所有选中的todo
      this.todos = this.todos.filter(todo => !todo.complete)
    },
    selectAllTodos (check) {
      // 全选或者全不选
      // eslint-disable-next-line no-return-assign
      this.todos.forEach(todo => todo.complete = check)
    }
  },
  components: {
    TodoHeader,
    TodoList,
    TodoFooter
  }
}
</script>

<style scoped>

  /*app*/
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

</style>
