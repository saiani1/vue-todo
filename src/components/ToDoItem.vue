<script setup lang="ts">
defineProps<{
  content: string
  checked: Boolean
}>()

const emits = defineEmits(['delItem'])

const handleClickDelBtn = (e: MouseEvent) => {
  const target = e.target as HTMLButtonElement
  const id = target.name
  emits('delItem', id)
}
</script>

<template>
  <div class="todoItemWrap">
    <div class="leftWrap">
      <input type="checkbox" :value="checked" />
      <p class="todoText">{{ content }}</p>
    </div>
    <button type="button" class="delBtn" :name="content" @click="handleClickDelBtn">X</button>
  </div>
</template>

<style lang="scss" scoped>
@import './todoItem.module.scss';
</style>
