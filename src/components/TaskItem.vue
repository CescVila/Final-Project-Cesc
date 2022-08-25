<template>
  <!-- <div v-for="(task, index) in taskData" :key="index"> -->
    <!-- <input v-else type="text" name="" id="" :placeholder="task.title" v-model="newTitle" /> -->
    <!-- <p v-if="!toggle">{{ task.description }}</p>
    <textarea v-if="toggle" name="" id="" cols="30" rows="10" :placeholder="task.description" v-model="newDescription"></textarea>
  <button v-if="toggle" @click="replaceButton(task.id)">Save changes</button>
    <div>
      <button v-if="!toggle" @click="toggleTask(task.id)">Remind</button>
      <button v-if="!toggle" @click="showInp" >Edit</button>
      <button @click="deleteTask(task.id)" v-if="!toggle">Delete</button>
    </div> -->
  <!-- </div> -->

  <div class="mt-10 mb-10">
  <div class="block p-6 rounded-lg shadow-lg bg-white max-w-sm">
    
    
    <h5 v-if="!toggle" class="text-gray-900 text-xl leading-tight font-medium mb-2">{{ task.title }}</h5>
    <input v-else type="text" name="" id="" :placeholder="task.title" v-model="newTitle" />
    <p v-if="!toggle" class="text-gray-700 text-base mb-4">{{ task.description }}
    </p>
    <textarea v-if="toggle" name="" id="" cols="30" rows="10" :placeholder="task.description" v-model="newDescription"></textarea>
    

    <button class="inline-block px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg transition duration-150 ease-in-out" v-if="toggle" @click="replaceButton(task.id)">Save changes</button>

    <button type="button" class=" inline-block px-6 py-2.5  text-white font-medium text-xs leading-tight uppercase rounded shadow-m  active:bg-black-800 active:shadow-lg transition duration-150 ease-in-out" :class="task.is_complete ? 'noToggle': 'showToggle'" v-if="!toggle" @click="toggleTask(task.id,!task.is_complete)">Remind</button>

    <button type="button" class=" inline-block px-6 py-2.5 bg-yellow-400 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-yellow-700 hover:shadow-lg focus:bg-yellow-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-yellow-800 active:shadow-lg transition duration-150 ease-in-out" v-if="!toggle" @click="showInp">Edit</button>

    <button type="button" class=" inline-block px-6 py-2.5 bg-red-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-red-700 hover:shadow-lg focus:bg-red-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-red-800 active:shadow-lg transition duration-150 ease-in-out" @click="deleteTask(task.id)" v-if="!toggle">Delete</button>
  </div>
</div>
</template>

<script setup>
import {ref} from "vue";
import {useTaskStore} from "../stores/task";
const toggle = ref(false);
const showInp = () => {
  toggle.value = !toggle.value;
}

const newTitle = ref("");
const newDescription = ref("");

// const emit = defineEmits([
//   ENTER-EMITS-HERE
// ])
const replaceButton = async (id) => {
  await useTaskStore().editTask(newTitle.value, newDescription.value, id);
  await useTaskStore().fetchTasks();
  toggle.value = !toggle.value;


};
const deleteTask = async (id) =>{
  await useTaskStore().deleteTask(id);
    await useTaskStore().fetchTasks();
};
const toggleTask = async (id,bool) =>{
  await useTaskStore().toggleTask(id,bool);
    await useTaskStore().fetchTasks();
    // if (bool) {document.getElementsByClassName("showToggle").innerHTML = "Done"}
    // else {document.getElementByClassName("noToggle").innerHTML ="To Do"}
};
// const props = defineProps({taskData: Object});
const props = defineProps({ task: Object });
</script>

<style scoped>
.showToggle{
background: orange ;
}
.noToggle{
background: green;
}
</style>

<!-- 
// **Hints**
// 1. ref() or reactive() can be used here to store the following, think if you want to store them either individually or like an object, up to you.
// 2. Data properties need here are the following: a boolean to store a false**Important variable, a string to store an error, a string to store the value of the task that the user can edit, an initial false boolean to hide the inputFIeld used to edit the new task detail or details[this is in reference of the task title and the task description].
// 3. Store the custom emit events that will be used to call the functions of the homeView for editing, deleting and toggling the status[completed, not complted] of the taskItem.
// 4. Function to handle the error with the data properties used to control the error and the the boolean controlling the boolean empty variable.
// 5. Function to handle the edit dialogue where the inputField is displayed and the string used to store the value of the inputField will be used here to save the value as a prop on this function.
// 6. Function to emmit a custom event emit() that takes 2 parameters a name for the custom event and the value that will be send via the prop to the parent component. This function can control the toggle completion of the task on the homeview.
// 7. Function to edit the task information that you decided that the user can edit. This function's body takes in a conditional that first checks if the value of the task [either title and description or just title] is empty which if true it runs the function used to handle the error on hint4. Else, the conditional sets the first mentioned boolean data property on hint2 back to its inital boolean value to hide the error message and repeat the same for the data property mentioned 4th on hint2; a constant that stores an object that holds the oldValue from the prop item and the value of the task coming from the data property mentioned 3rd on hint2; a custom event emit() that takes 2 parameters a name for the custom event and the value from the object used on this part of the conditional and lastly this part of the conditional sets the value of input field to an empty string to clear it from the ui. 
// 8. Function to emmit a custom event emit() that takes 2 parameters a name for the custom event and the value that will be send via the prop to the parent component. This function can control the removal of  the task on the homeview.
// -->
