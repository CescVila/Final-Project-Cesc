<template>
  <Nav />

  <NewTask @taskToAdd="callTask" />

  <div class="flex flex-wrap gap-6 justify-around m-auto">
    <div v-for="task in setTask.tasks" :key="task.id">
      <TaskItem :task="task" />
    </div>
  </div>
  <Footer class="fixed inset-x-0 bottom-0" />
  
</template>

<script setup>
import Nav from "../components/Nav.vue";
import NewTask from "../components/NewTask.vue";
import { useTaskStore } from "../stores/task";
import { ref } from "vue";
import { supabase } from "../supabase/";
import Footer from "../components/Footer.vue";
import TaskItem from "../components/TaskItem.vue";

const setTask = useTaskStore();

setTask.fetchTasks();

async function callTask(task) {
  await setTask.addTask(task.name, task.description);
  setTask.fetchTasks();
}


</script>

<style></style>


