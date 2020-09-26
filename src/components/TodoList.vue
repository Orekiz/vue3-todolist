<template>
  <div class="todolist">
    <ul>
      <li
        v-for="(item, index) of todoList"
        :key="index">
        <input
          type="checkbox"
          :checked="item.completed"
          @click="setCompleted(item.id)"
        />
        <span
          :style="{ 'text-decoration': item.completed ? 'line-through' : 'none' }"
        >
          {{ item.content }}
        </span>
        <button
          @click="removeTodoItem(item.id)"
        >
          删除
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  props: {
    todoList: Array
  },
  setup (props, ctx) {
    const setCompleted = id => {
      ctx.emit('set-completed', id)
    }

    const removeTodoItem = id => {
      ctx.emit('remove-todo-item', id)
    }

    return {
      setCompleted,
      removeTodoItem
    }
  }
}
</script>

<style lang="less" scoped>

</style>
