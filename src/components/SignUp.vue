<template>
  <div class="containerUp">
    <div class="headingUp">      
      <PersonalRouter :route="route" :buttonText="buttonText" />
      <form @click.prevent="signUp">
        <div class="inpEmail">

        </div>
         <label for="email">Email</label>
        <input type="text" v-model="email" placeholder="Email"/>
        <br>
         <label for="password">Password</label>
        <input type="password" v-model="password" placeholder="******"/>
        <br>
         <label for="password" >Confirm password</label>
        <input type="password" v-model="password" placeholder="******"/>
        <br>
        <input type="submit" />
      </form>
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

// Route Variables
const route = "/auth/login";
const buttonText = "Sign In Route";

// Input Fields

const email = ref("");
const password = ref("");

// Error Message
const errorMsg = ref("");

// Show hide password variable
const passwordFieldType = computed(() =>
  hidePassword.value ? "password" : "text"
);

// Show hide confrimPassword variable
const hidePassword = ref(true);

// Router to push user once SignedUp to Log In
const redirect = useRouter();

// Arrow function to SignUp user to supaBase with a timeOut() method for showing the error

const signIn = async () => {
  try {
    // calls the user store and send the users info to backend to logIn
    await useUserStore().signIn(email.value, password.value);
    // redirects user to the homeView
    redirect.push({ path: "/" });
  } catch (error) {
    // displays error message
    errorMsg.value = `Error: ${error.message}`;
    // hides error message
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  }
};
</script>

<style>
.containerUp{
  display: flex;

}

</style>
