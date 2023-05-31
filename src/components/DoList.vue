<script setup lang="ts">
import { defineProps } from 'vue'
import { ref, defineEmits } from 'vue'

export interface Props {
  doList: Array<{ id: string; contents: string; status: 'active' | 'clear' }>
}
const props = withDefaults(defineProps<Props>(), {
  doList: () => []
})

const emit = defineEmits<{
  changeItem: [id: string]
  removeItem: [id: string]
}>()

const check = (id: string) => {
  emit('changeItem', id)
}
</script>

<template>
  <div v-for="item in props.doList" :key="item.id" class="container">
    <input type="checkbox" :checked="item.status === 'clear'" @change="check(item.id)" />
    <div>
      <div :class="item.status === 'clear' ? 'finish' : ''">{{ item.contents }}</div>
      <span @click="$emit('removeItem', item.id)">삭제</span>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  padding: 5px 0;
}
.container > input {
  margin-right: 10px;
}
.container > div {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}
.container > div > span {
  font-size: 12px;
  color: red;
  cursor: pointer;
}
.finish {
  text-decoration: line-through;
  color: #aaa;
}
</style>
