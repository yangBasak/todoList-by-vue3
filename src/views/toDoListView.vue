<script setup lang="ts">
import DoList from '../components/DoList.vue'
import { v4 } from 'uuid'
import { ref } from 'vue'
const inputContent = ref('')

interface ListItem {
  id: string
  contents: string
  status: 'active' | 'clear'
}
const doList = ref([] as ListItem[])

const addItem = () => {
  doList.value.push({
    id: v4(),
    contents: inputContent.value,
    status: 'active'
  })
  inputContent.value = ''
}
const removeItem = (id: string) => {
  const findIdx = doList.value.findIndex((item) => {
    return item.id === id
  })
  doList.value.splice(findIdx, 1)
}
const changeStatus = (id: string) => {
  const findIdx = doList.value.findIndex((item) => {
    return item.id === id
  })

  if (doList.value[findIdx].status === 'active') doList.value[findIdx].status = 'clear'
  else doList.value[findIdx].status = 'active'
}
</script>

<template>
  <div class="todo-component">
    <div class="search-box">
      <input type="text" v-model="inputContent" placeholder="할일을 입력해주세요." />
      <button @click="addItem">추가</button>
    </div>
    <DoList :doList="doList" @removeItem="removeItem" @changeItem="changeStatus" />
  </div>
</template>

<style scoped>
.todo-component {
  width: 80%;
  margin: auto;
}
.search-box {
  display: flex;
  width: 100%;
  height: 40px;
  margin: 5px 0;
}
.search-box input {
  height: 100%;
  width: 100%;
}
.search-box button {
  height: 100%;
  width: 70px;
  margin-left: 5px;
  border: none;
  background-color: cadetblue;
  color: #fff;
}
</style>
