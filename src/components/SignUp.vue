<template>
  
    <div>
		<!-- Container -->
		<div >
			<div class="flex justify-center px-6 my-12 ">
				<!-- Row -->
				<div class="w-full xl:w-3/4 lg:w-11/12 flex">
					<!-- Col -->
					<div
						class=" h-auto bg-gray-400 hidden lg:block lg:w-5/12 bg-cover rounded-l-lg "
						style="background-image: url('https://cdn.shopify.com/s/files/1/0232/3936/0576/products/Metallicgearssteampunklargeprint_900x.jpg?v=1585249093')"
					></div>
					<!-- Col -->
					<div class="w-3/4 bg-white p-5 rounded-lg lg:rounded-l-none">
						<div class="headingIn my-auto mt-5 py-10 px-10">
      <h1 class="text-6xl flex justify-center mb-4">Welcome</h1>
      <h2 class="text-3xl flex justify-center mt-2 mb-14">Register to acces</h2>

      <div class="flex justify-center">
         <form class="w-2/3 flex flex-col" @submit.prevent="signUp">
        
        
         <label class="text-2xl mb-1 flex justify-center" for="email">Email</label>
         <br>
        <input class="borderInput mb-6" type="text" v-model="email" placeholder="email@gmail.com" id="email" required/>  
        <br>
         <label class="text-2xl mb-1 flex justify-center" for="password">Password</label>
         <br>
        <input class="borderInput mb-6" type="password" v-model="password" placeholder="******" id="password" required/>
        <br class="">
         <label class="text-2xl mb-1 flex justify-center" for="password" >Confirm password</label>
         <br>
        <input class="borderInput" type="password" v-model="confirmPassword" placeholder="******" id="confirmPassword" required/>
        <br>
        <input class="inline-block px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-600 hover:shadow-lg focus:bg-blue-400 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-500 active:shadow-lg transition duration-150 ease-in-out mb-8 " type="submit" required/>
      </form>
        
      </div>
      <div class="text-2xl flex justify-center mt-1"><PersonalRouter :route="route" :buttonText="buttonText" /></div>
    </div>
					</div>
				</div>
			</div>
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
const confirmPassword= ref("");

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

const signUp = async () => {
  if(password.value === confirmPassword.value){
  try {
    // calls the user store and send the users info to backend to logIn
    await useUserStore().signUp(email.value, password.value);
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
  return;
  }
  errorMsg.value = "Password not the same";
};
</script>

<style>
.borderInput{
  border: 3px solid rgb(26, 144, 187);
}
</style>
