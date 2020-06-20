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
      // 从localStorage 读取todo
      // parse解析JSON
      todos: JSON.parse(window.localStorage.getItem('todos_key') || '[]')
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

  watch: {
    // 监视
    todos: {
      deep: true, // 深度监视
      handler: function (Value) {
        // 将todos最新的JSON数据保存到localStorage
        // stringify 转为JSON
        window.localStorage.setItem('todos_key', JSON.stringify(Value))
      }
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
