<template>
  <header class="header">
    <h1>todos</h1>
    <input
        v-model.trim="content"
        class="new-todo" placeholder="What needs to be done?"
        autofocus @keydown.enter="add"/>
  </header>
</template>

<script setup>
import { v4 as uuidv4 } from 'uuid';
import { ref } from 'vue'

const content = ref('')
const emit = defineEmits(['addList'])
const add = () => {
  // 校验
  if (!content.value) {
    return alert('内容不能为空')
  }
  const str = {
    id: uuidv4(),
    name: content.value,
    done: false,
  }
  emit('addList', str)
  //清空
  content.value = ''
}
</script>

<style lang="less" scoped></style>
