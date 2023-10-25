<script setup lang="ts">
import { ref } from 'vue'
import ToDoItem from './components/ToDoItem.vue'
import { todoData } from './assets/data/todoData'

const todoDataArr = ref(todoData)
const insertTodo = ref('')

const delItem = (id: string) => {
  todoDataArr.value = todoDataArr.value.filter((item) => {
    return item.content !== id
  })
}

const onSubmit = () => {
  todoDataArr.value.unshift({
    content: insertTodo.value,
    id: todoDataArr.value.length + 1,
    checked: false
  })
  insertTodo.value = ''
}
</script>

<template>
  <header class="header">TO DO LIST</header>
  <section>
    <div class="todoWrap">
      <form class="inputWrap" @submit.prevent="onSubmit">
        <input type="text" id="textinput" placeholder="Insert your To do" v-model="insertTodo" />
        <button type="submit" class="submitBtn">
          <span>입력</span>
        </button>
      </form>
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
