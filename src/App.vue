<script setup lang="ts">
import { ref } from 'vue'
import ToDoItem from './components/ToDoItem.vue'
import { todoData } from './assets/data/todoData'

const todoDataArr = ref(todoData)

const delItem = (id: string) => {
  todoDataArr.value = todoDataArr.value.filter((item) => {
    return item.content !== id
  })
}
</script>

<template>
  <header class="header">TO DO LIST</header>
  <section>
    <div class="todoWrap">
      <div class="inputWrap">
        <input type="text" id="textinput" placeholder="Insert your To do" />
        <button type="button" class="submitBtn"><span>입력</span></button>
      </div>
      <div class="todoListWrap">
        <ToDoItem
          v-for="{ id, content, checked } in todoDataArr"
          :key="id"
          :content="content"
          :checked="checked"
          @delItem="delItem"
        />
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@import './app.module.scss';
</style>
