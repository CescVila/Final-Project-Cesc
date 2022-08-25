<template> 
  <nav class="flex justify-between navbar">
    <div class="w-12">
      <img src="https://png2.cleanpng.com/sh/848a560ab051b57ae7cbb7c7fd90a6bd/L0KzQYi4UsE3N5U3TJGAYUO3drKBVcVkPmE5UZC6OEG8Q4S3VME2OWQ5SqM9NEW2R4m7TwBvbz==/5a34fa855c6049.1819330415134214453784.png" class="w-full" alt="">
    </div>
    <h1 class="font-bold text-2xl mt-2">Welcome to your Tasksboard</h1>
    <button @click="signOut" class="inline-block px-6 py-2.5 bg-green-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-green-600 hover:shadow-lg focus:bg-green-400 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-green-500 active:shadow-lg transition duration-150 ease-in-out">Log out</button>
    
  </nav>
</template>

<script setup>
import PersonalRouter from "./PersonalRouter.vue";
import { ref, computed } from "vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";

//constant to save a variable that will hold the use router method


// const route = "/auth/login";

// constant to save a variable that will get the user from store with a computed function imported from vue
const userStore = useUserStore();
// constant that calls user email from the useUSerStore
const email =userStore.user.email;
// constant that saves the user email and cleans out the @client from the user
const name = email.split("@");
// async function that calls the signOut method from the useUserStore and pushes the user back to the Auth view.

const errorMsg = ref("");
const redirect = useRouter();
const signOut = async () => {
  try {
    // calls the user store and send the users info to backend to logIn
    await useUserStore().signOut();
    // redirects user to the homeView
    redirect.push({ path: "/auth/login" });
  } catch (error) {
    // displays error message
    errorMsg.value = error.message;
    // hides error message
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  }
  };
  
  

</script>

<style scoped>
.navbar{
  background: #f1f1f1;
  padding: 20px 150px;
}
</style>
