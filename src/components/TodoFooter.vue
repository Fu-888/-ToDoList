<template>
  <footer class="footer">
    <span class="todo-count"><strong>{{ listLength }}</strong> item left</span>
    <ul class="filters">
      <li v-for="item in stateList" :key="item.id">
        <a :class="{selected:item.id=== currentId}" :href="item.path"
           @click="emit('toggle',item.id)">{{ item.state }}</a>
      </li>
    </ul>
    <button class="clear-completed" @click="emit('clear')" v-show="show"
    >Clear completed
    </button>
  </footer>
</template>

<script setup>
import { computed, defineEmits, reactive } from 'vue'

const props = defineProps({
  list: Array,
  currentId: Number
})
// 未完成的长度
const listLength = computed(() => {
  return props.list && Array.from(props.list).reduce(
      (pre, item) => !item.done ? pre + 1 : pre, 0) || 0
})
// 状态数据
const stateList = reactive([
  { id: 1, state: 'All', path: '#/' },
  { id: 2, state: 'Active', path: '#/active' },
  { id: 3, state: 'completed', path: '#/Completed' },
])

// 是否显示的状态
const show = computed(() => {
  return props.list && Array.from(props.list).filter(item => item.done).length
})
const emit = defineEmits(['toggle', 'clear'])
</script>

<style lang="less" scoped></style>
