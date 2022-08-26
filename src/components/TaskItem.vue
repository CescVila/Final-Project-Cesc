<template>
  <div class="mt-10 mb-15">
  <div class="block p-6 rounded-lg shadow-lg bg-white max-w-sm">
    
    
    <h5 v-if="!toggle" class="text-gray-900 text-xl leading-tight font-medium mb-2">{{ task.title }}</h5>
    <input v-else type="text" name="" id="" :placeholder="task.title" v-model="newTitle" />
    <p v-if="!toggle" class="text-gray-700 text-base mb-4">{{ task.description }}
    </p>
    <textarea v-if="toggle" name="" id="" cols="30" rows="10" :placeholder="task.description" v-model="newDescription"></textarea>
    

    <button class="inline-block px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg transition duration-150 ease-in-out" v-if="toggle" @click="replaceButton(task.id)">Save changes</button>

    <button type="button" class=" inline-block m-1 px-6 py-2.5  text-white font-medium text-xs leading-tight uppercase rounded shadow-m  active:bg-black-800 active:shadow-lg transition duration-150 ease-in-out" :class="task.is_complete ? 'noToggle': 'showToggle'" v-if="!toggle" @click="toggleTask(task.id,!task.is_complete)">{{ task.is_complete ? "completed" : "complete" }}</button>

    <button type="button" class=" inline-block m-1 px-6 py-2.5 bg-yellow-400 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-yellow-700 hover:shadow-lg focus:bg-yellow-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-yellow-800 active:shadow-lg transition duration-150 ease-in-out" v-if="!toggle" @click="showInp">Edit</button>

    <button type="button" class=" inline-block m-1 px-6 py-2.5 bg-red-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-red-700 hover:shadow-lg focus:bg-red-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-red-800 active:shadow-lg transition duration-150 ease-in-out" @click="deleteTask(task.id)" v-if="!toggle">Delete</button>
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
};

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
