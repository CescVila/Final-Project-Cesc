<template> 
  <nav class="flex justify-between navbar">
    <div class="w-12">
      <img src="https://png2.cleanpng.com/sh/848a560ab051b57ae7cbb7c7fd90a6bd/L0KzQYi4UsE3N5U3TJGAYUO3drKBVcVkPmE5UZC6OEG8Q4S3VME2OWQ5SqM9NEW2R4m7TwBvbz==/5a34fa855c6049.1819330415134214453784.png" class="w-8 h-9 pt-2" alt="">
    </div>
    <h1 class="font-bold text-2xl pt-2">Welcome to your Tasksboard</h1>
    <div>
      <h2 class="font-bold text-2xl pt-2">Hello {{name[0]}}</h2>
    </div>
    <button @click="signOut" class="inline-block px-5 py-1 bg-green-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-green-600 hover:shadow-lg focus:bg-green-400 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-green-500 active:shadow-lg transition duration-150 ease-in-out">Log out</button>
    
  </nav>
</template>

<script setup>
import PersonalRouter from "./PersonalRouter.vue";
import { ref, computed } from "vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";

const userStore = useUserStore();

const email =userStore.user.email;

const name = email.split("@");

const errorMsg = ref("");
const redirect = useRouter();
const signOut = async () => {
  try {
   
    await useUserStore().signOut();
    
    redirect.push({ path: "/auth/login" });
  } catch (error) {
   
    errorMsg.value = error.message;
    
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  }
  };
  
  

</script>

<style scoped>
.navbar{
  background: rgb(242, 250, 240);
  padding: 1px 280px;
}
</style>
