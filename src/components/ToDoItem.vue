<script setup lang="ts">
import { ref } from 'vue'
const Props = defineProps<{
  content: string
  checked: Boolean
}>()

const isModify = ref(false)
const itemContent = ref(Props.content)

const emits = defineEmits(['delItem'])

const handleClickModifyBtn = () => {
  isModify.value = !isModify.value
}

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
      <template v-if="!isModify">
        <p class="todoText">{{ itemContent }}</p>
      </template>
      <template v-else>
        <input type="text" v-model="itemContent" />
      </template>
    </div>
    <div class="btnWrap">
      <button type="button" class="modifyBtn" @click="handleClickModifyBtn">
        {{ !isModify ? '수정' : '저장' }}
      </button>
      <button type="button" class="delBtn" :name="content" @click="handleClickDelBtn">X</button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import './todoItem.module.scss';
</style>
