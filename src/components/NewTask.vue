<template>
  <div>New Task Component</div>
  <div>
    <span></span>
    <h2>Add a new Task</h2>
    <h3>
      Keep your life organized, prepare for a trip ? Start here Today's Date is
      Aug 22nd 2022
    </h3>
  </div>
  <div>
    <div>
      <div v-if="showError"> {{errorMsg}}
      </div>
      <!-- <form @submit.prevent="toAdd"> -->
        <input type="text" placeholder="Add a Task Title" v-model="taskName" />
        <input type="text" placeholder="Add a Taks Description" v-model="taskDescription" />
        <button @click="toAdd">Add</button>
      <!-- </form> -->
    </div>
  </div>  
</template>

<script setup>
import PersonalRouter from "./PersonalRouter.vue";
import { ref, computed } from "vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";
import { useTaskStore } from "../stores/task";

// constant to save a variable that define the custom event that will be emitted to the homeView
const emit = defineEmits(["taskToAdd"]);
// constant to save a variable that holds the value of the title input field of the new task
const taskName = ref("");
// constant to save a variable that holds the value of the description input field of the new task
const taskDescription = ref("");
// constant to save a variable that holds an initial false boolean value for the errorMessage container that is conditionally displayed depending if the input field is empty
const showError = ref(false);
// const constant to save a variable that holds the value of the error message
const errorMsg = ref(null);
// arrow function to call the form holding the task title and task description that uses a conditional to first checks if the task title is empty, if true the error message is displayed through the errorMessage container and sets a timeOut method that hides the error after some time. Else, its emmits a custom event to the home view with the task title and task description; clears the task title and task description input fields.
function toAdd(){
  if (taskName.value.length === 0 || taskDescription.value.length === 0) {
    showError.value = true;
    errorMsg.value = "You must fill both fields";
      setTimeout(() => {
        showError.value = false;
    }, 5000);
  }
const newAdd = {
  name: taskName.value,
  description: taskDescription.value,
};

emit("taskToAdd", newAdd);
taskName.value = "";
taskDescription.value = "";
}


// const toAdd = async () => {
//   if (taskName.value === "") {
//     try {
//       // calls the user store and send the users info to backend to logIn
//       await useTaskStore().addTask(taskName.value, taskDescription.value);
//       task.value = null;
//       taskDescription.value = null;
//     } catch (error) {
//       // displays error message
//       errorMsg.value = error.message;
//       // hides error message
//       setTimeout(() => {
//         errorMsg.value = null;
//       }, 5000);
//     }
//     return;
//   }
//   errorMsg.value = "Password not the same";
// };
</script>

<style></style>
