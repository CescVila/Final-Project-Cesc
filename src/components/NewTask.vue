<template>
  <div class="backgroundNewTask m-auto mt-20 w-3/6 py-10 px-10">
    <div class="flex justify-around">
      <div class="">
        <span></span>
        <h2 class="font-sans text-6xl mt-5 mb-10 flex justify-center font-bold" >Add a new Task</h2>
        <h3 class="font-sans text-2xl mt-5 mb-10 flex justify-center font-bold">
          Keep your life organized. Start here Today's Date
          is Aug 26th 2022
        </h3>
      </div>
    </div>

    
  </div>
   <div class="flex m-auto ">
      <div class="flex justify-between mt-5 mb-15">
        <div v-if="showError">{{ errorMsg }}</div>
        <!-- <form @submit.prevent="toAdd"> -->
        <input
          class="px-2 py-2 m-8 borderInput border-green-400"
          type="text"
          placeholder="Add a Task Title"
          v-model="taskName"
        />
        <input
          class="px-2 py-2 m-8 borderInput border-green-400"
          type="text"
          placeholder="Add a Taks Description"
          v-model="taskDescription"
        />
        

        <!-- </form> -->
      </div>

      <div class="my-auto">
          <button
            @click="toAdd"
            class="inline-block p-4 mt-5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg transition duration-150 ease-in-out"
          >
            Add
          </button>
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
function toAdd() {
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

<style>
.backgroundNewTask{
  background-color: white;
  

}
.borderInput{
  border: 3px solid rgb(18, 214, 38);
}

</style>
