<script setup lang="ts">
import { Ref, ref } from "vue";

type Todo = { info: string; currency: "PLN" | "EUR" | "USD" };

const options = ref(["PLN", "EUR", "USD"]);

const currency: Ref<"PLN" | "EUR" | "USD"> = ref("PLN");
const info = ref("");

const todos: Ref<Todo[]> = ref([]);

const addTodo = () => {
  const newTodo: Todo = {
    info: info.value,
    currency: currency.value,
  };
  todos.value.push(newTodo);
};

const deleteTodo = (todo: Todo) => {
  todos.value = todos.value.filter((singleTodo) => singleTodo !== todo);
};
</script>

<template>
  <main class="grid place-items-center">
    <div class="flex flex-col gap-2 w-80">
      <form @submit.prevent="addTodo" class="flex gap-1">
        <input
          maxlength="18"
          required
          v-model="info"
          placeholder="Set your todo"
          class="px-2 py-1 bg-transparent border-black dark:border-green-300 border-2 rounded-l-full dark:text-white"
        />

        <select
          v-model="currency"
          class="p-1 bg-transparent border-black border-2 dark:text-white dark:border-green-300"
        >
          <option v-for="option in options" :value="option">
            {{ option }}
          </option>
        </select>

        <button
          type="submit"
          class="bg-white dark:bg-green-300 hover:bg-green-200 focus:bg-green-200 dark:focus:bg-green-300 dark:hover:focus:bg-green-300 border-black border-2 rounded-r-full px-2 py-1"
        >
          Add
        </button>
      </form>
      <ul class="flex flex-col gap-2" v-if="todos.length">
        <li
          v-for="todo in todos"
          class="dark:text-white flex align-center border-black dark:border-green-300 border-2 py-1 pl-2 pr-1 justify-between rounded-lg"
        >
          {{ todo.info }} - {{ todo.currency }}
          <button @click="deleteTodo(todo)">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </li>
      </ul>
      <div v-else class="opacity-50 text-center">No TODOs to show</div>
    </div>
  </main>
</template>
