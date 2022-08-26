<template>
  <section class="main">
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll"/>
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <li :class="{completed:item.done}" v-for="item in newList" :key="item.id">
        <div class="view">
          <input class="toggle" type="checkbox" checked v-model="item.done"
          />
          <label>{{ item.name }}</label>
          <button class="destroy" @click="emit('del',item.id)"></button>
        </div>
        <input class="edit" value="Create a TodoMVC template"/>
      </li>
    </ul>
  </section>
</template>

<script setup>
import { computed, watch } from 'vue'

const props = defineProps({
  list: {
    type: Array,
    default: () => []
  },
  currentId: Number
})
// 全选和反选的状态
const isAll = computed({
  get () {
    return props.list && Array.from(props.list).every(item => item.done)
  },
  set (val) {
    Array.from(props.list).forEach(item => item.done = val)
  }
})
const emit = defineEmits(['changeState', 'del'])
// 根据显示的ID,显示不同的数据列表
const newList = computed(
    () => {
      if (props.currentId === 2) {
        return props.list.filter(item => !item.done)
      } else if (props.currentId === 3) {
        return props.list.filter(item => item.done)
      } else if (props.currentId === 1) {
        return props.list
      } else {
        return []
      }
    }
)

</script>

<style lang="less" scoped></style>
