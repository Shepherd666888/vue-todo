<script setup lang="ts">
import { ref } from 'vue';
interface TodoItem {
  id: number;
  text: string;
}
const input = ref('');
const todoList = ref<TodoItem[]>([]);
let count = 0;
const add = () => {
  if (input.value.trim() === '') {
    alert('oi,没有输入啊喂！');
    return;
  }
  count++;
  todoList.value.push({
    id: count,
    text: input.value,
  });
  input.value = '';
};
const del = (id: number) => {
  todoList.value = todoList.value.filter((item) => item.id !== id);
};

const clear = () => {
  todoList.value = [];
};
</script>

<template>
  <div class="container">
  <img src="@/assets/picture/初音1.jpg" alt="picture" width="125" height="125">
    <div class="header"><h1>Todo List</h1></div>
     <div class="input-box">
      <input
        v-model="input"
        @keyup.enter="add"
        placeholder="输入你要做的事"
      />
      <button @click="add">添加</button>
    </div>
    <ul v-if="todoList.length > 0" class="todo-list">
      <li v-for="item in todoList" :key="item.id" class="todo-item">
        <span>{{ item.text }}</span>
        <button class="del" @click="del(item.id)">删除</button>
      </li>
    </ul>

    <p v-else class="empty"> 暂无待办</p >

    <button v-if="todoList.length > 0" @click="clear" class="clear">
      清空列表
    </button>
  </div>
</template>

<style scoped>
.container {
  max-width: 500px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #dddddd;
  border-radius: 8px;
  font-family: sans-serif;
  text-align: center;
}
.header {
  border-radius: 14px;
  margin-bottom: 20px;
  font-family: 'Arial Black', Gadget, sans-serif;
  background: #359c6c;
  color: white;
  border: 15px solid #4fc27b;
}

.input-box {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  border-radius: 10px;
  padding: 8px 15px;
  background-color: #42b883;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #359c6c;
}

.todo-list {
  list-style: none;
  padding: 0;
  text-align: left;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #eee;
}

.del {
  background-color: #7a080a;
}
.del:hover {
  background-color: #8c1117;
}

.empty{
  color: #999;
  margin-top: 20px;
}

.clear{
  margin-top: 20px;
  background-color: #999;
}
</style>
