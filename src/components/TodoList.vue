<template>
  <div class="todo-list">
    <h2>ToDo 리스트</h2>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        {{ todo }}
        <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
    <form @submit.prevent="addTodo">
      <input v-model="newTodo" placeholder="New ToDo" />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script setup>
// Vue에서 반응형 배열과 참조를 가져옵니다.
import { reactive, ref } from 'vue';

// todos는 빈 배열로 초기화된 반응형 배열입니다.
const todos = reactive([]);
// newTodo는 빈 문자열로 초기화된 참조입니다.
const newTodo = ref('');

const addTodo = () => {
  if (newTodo.value) {
    todos.push(newTodo.value);
    newTodo.value = '';
  }
};

const removeTodo = (index) => {
  todos.splice(index, 1);
};
</script>

<style scoped>
.todo-list {
  max-width: 400px;
  margin: 0 auto;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding: 10px;
  border-bottom: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

input {
  width: calc(100% - 60px);
  padding: 5px;
}

button {
  padding: 5px 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}
</style>
