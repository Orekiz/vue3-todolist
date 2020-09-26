<template>
  <TodoInput
    @add-todo-item="addTodoItem"
  />
  <TodoList
    :todoList="todoList"
    @set-completed="setCompleted"
    @remove-todo-item="removeTodoItem"
  />
</template>

<script>
import TodoInput from './components/TodoInput'
import TodoList from './components/TodoList'

import { reactive, toRefs } from 'vue'
export default {
  name: 'App',
  components: {
    TodoInput,
    TodoList
  },
  setup () {
    const state = reactive({
      todoList: []
    })

    const addTodoItem = (addTodoItem) => {
      state.todoList.push(addTodoItem)
      console.log(state.todoList)
    }

    const setCompleted = id => {
      state.todoList = state.todoList.map(item => {
        if (item.id === id) {
          item.completed = !item.completed
        }
        return item
      })
    }

    const removeTodoItem = id => {
      // 箭头函数写一行，省略 'return' = return item.id !== id
      state.todoList = state.todoList.filter(item => item.id !== id)
    }

    return {
      ...toRefs(state), // 拓展
      addTodoItem,
      setCompleted,
      removeTodoItem
    }
  }
}
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
