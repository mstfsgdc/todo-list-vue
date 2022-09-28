<script setup>

</script>

<template>
  <main>
    <div class="add-todo">
      <form @submit.prevent="addTodo" class="add-box">
        <input v-model="todoInput" type="text" placeholder="Add Task" minlength="5" autofocus />
        <input type="submit" value="Add" />
      </form>
    </div>
    <div class="todos">
      <div v-for="todo in todos" :key="todo.id" class="todo-card" :class="{ done: todo.done }" @click="toggleStatus(todo)">
        <h2>{{todo.taskName}}</h2>
      </div>
    </div>
  </main>
</template>

<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const todoInput = ref('');
      const todos = ref([]);

      const addTodo = () => {
        if(todoInput.value != "") {
          todos.value.push({
            done: false,
            taskName: todoInput.value,
            id: Date.now(),
          });
          todoInput.value = '';
        }
        saveTodos();
      }

      const loadTodos = () => {
        const values = JSON.parse(localStorage.getItem('todos'));
        if(values) todos.value.push(...values);
      }

      const saveTodos = () => {
        localStorage.setItem('todos', JSON.stringify(todos.value));
      }

      const toggleStatus = (todo) => {
        todo.done = !todo.done;
        saveTodos();
      }

      return {
        todoInput,
        todos,
        addTodo,
        toggleStatus,
        loadTodos,
      }
    },
    created() {
      this.loadTodos()
    }
  }
</script>

<style lang="scss">
body {
  background: linear-gradient(45deg, #7d84b2 0%, lighten(#7d84b2, 7%) 100%);
}

.add-todo {
  background-color: rgba(250, 235, 215, 0.63);
  padding: .5rem;
  margin: .75rem .5rem .75rem .5rem;
  border-radius: .5rem;

  form {
    display: flex;
    justify-content: space-evenly;

    input[type="submit"] {
      margin: 0 .5rem 0 .5rem;
    }

    input[type="text"] {
      width: 100%;
      border-radius: .25rem;
      padding: .125rem;
      background-color: transparent;
      border: none;

      &:focus, &:active, &:focus-visible {
        border: none;
        outline: none;
      }
    }
  }
}

.todos {
display: flex;
flex-direction: column-reverse;
}

.todo-card {
  border: 1px solid rgba(204, 204, 204, 0.5);
  border-radius: .25rem;
  margin: .5rem 1rem .5rem 1rem;
  padding: 0 .25rem 0 .25rem;
  display: flex;
  align-items: center;
  cursor: pointer;
  width: fit-content;

  transition: filter, background-color, color 0.2s ease-in;

  h2 {
    font-size: 1rem;
    font-weight: normal;
  }

  &.done {
    filter: blur(2px) opacity(50%);
    background-color: lightgreen;
    color: white;
  }
}
</style>
