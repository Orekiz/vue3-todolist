<template>
  <div class="todoinput">
    <input type="text" v-model="todoValue" @input="updateTodoValue($event)">
    <button @click="addTodoItem()">+</button>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  name: 'TodoInput',
  setup (props, ctx) {
    const todoValue = ref('')
    const updateTodoValue = (e) => {
      todoValue.value = e.target.value
    }
    function addTodoItem () {
      // 去除空格
      const _val = todoValue.value.trim()

      // 长度为0直接返回
      if (_val.length === 0) {
        // eslint-disable-next-line no-useless-return
        return
      }

      // 向父组件emit这个方法 = 以前this.$emit
      // 事件名必须是 kebab-case (短横隔开式)
      ctx.emit('add-todo-item', {
        id: new Date().getTime(),
        content: _val,
        completed: false
      })

      // 提交后清空输入框
      todoValue.value = ''
    }

    return {
      todoValue,
      updateTodoValue,
      addTodoItem
    }
  }
}
</script>

<style lang="less" scoped>

</style>
