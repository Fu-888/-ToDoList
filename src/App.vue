<template>
  <section class="todoapp">
    <TodoHeader @addList="addList"></TodoHeader>
    <TodoMain :list="list" @del="del" :currentId="currentId"></TodoMain>
    <TodoFooter :list="list" @toggle="toggle" :currentId="currentId" @clear="clear"></TodoFooter>
  </section>
</template>

<script setup>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'
import { reactive, ref, watch } from 'vue'

const currentId = ref(1)
// 显示的壮态ID
const toggle = (id) => {
  currentId.value = id
}
// 提供数据
const list = ref([]) && ref(JSON.parse(localStorage.getItem('todoList')))
// console.log(list.value)
// 添加数据
const addList = (val) => {
  list.value.unshift(val)
}

// 删除点击当前项
const del = (id) => {
  // console.log(id)
  list.value.forEach((item, i) => {
    if (item.id === id) {
      list.value.splice(i, 1)
    }
  })
}
//当list发生变化的时候,存储起来
watch(list, (newList) => {
  // console.log(newList)
  localStorage.setItem('todoList', JSON.stringify(list.value))
}, {
  deep: true,
  immediate: true,
})
//清除已经完成的
const clear = () => {
  list.value = list.value.filter((item) => !item.done)
}

</script>

<style></style>
