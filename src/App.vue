<template>
  <Button>
    <strong>Demo</strong>
    de bouton
  </Button>
  <hr />
  <Layout>
    <!-- v-slot:header peut être ecrit comme ceci : #header -->
    <template #header> En tête </template>
    <template #aside> sidebar </template>
    <template #main> main </template>
    <template #footer> footer </template>
  </Layout>
  <hr />
  <form action="" @submit.prevent="addTodo">
    <input
      v-model="newTodo"
      type="text"
      name="todo"
      placeholder="Entrer une taches"
    />
    <button type="submit" @click.prevent="addTodo">Ajouter</button>
  </form>
  <div v-if="todos.length == 0">Aucune tâche disponible.</div>
  <div v-else>
    <ul>
      <li
        v-for="(todo, index) in sortedTodos"
        :key="index"
        :class="{ completed: todo.completed }"
      >
        <Checkbox
          :label="todo.title"
          v-model="todo.completed"
          @check="console.log('coché')"
          @uncheck="console.log('non coché')"
        />
      </li>
    </ul>
  </div>
  <p v-if="remainingTodos > 0">
    {{ remainingTodos }} tache{{ remainingTodos > 1 ? "s" : "" }} à faire
  </p>
  <div>
    <label>
      <input v-model="hideCompleted" type="checkbox" />
      Masquer les tâches complétées
    </label>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
import Checkbox from "./Checkbox.vue";
import Button from "./Button.vue";
import Layout from "./Layout.vue";

const todos = ref([
  {
    title: "Tache à faire",
    completed: true,
    date: 1020302103,
  },
]);
const newTodo = ref("");
const hideCompleted = ref(false);

const addTodo = () => {
  if (newTodo.value.trim() !== "") {
    todos.value.push({
      title: newTodo.value,
      completed: false,
      date: Date.now(),
    });
    newTodo.value = "";
  }
};
const deleteTodo = (index) => {
  todos.value.splice(index, 1);
};

//---- 1 method
const sortedTodos = computed(() => {
  console.log("demo");

  const sorted = todos.value.toSorted((a, b) =>
    a.completed > b.completed ? 1 : -1
  );

  if (hideCompleted.value) {
    return sorted.filter((todo) => !todo.completed);
  }

  return sorted;
});

// 2 method
// const sortedTodos = computed(() => {
//   return todos.value.slice().sort((a, b) => a.completed - b.completed);
// });

const remainingTodos = computed(() => {
  return todos.value.filter((todo) => todo.completed == false).length;
});
console.log(remainingTodos);
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: gray;
}
</style>
