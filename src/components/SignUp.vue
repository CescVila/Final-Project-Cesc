<template>
  <div>
    
    <div>
      <div class="flex justify-center px-6 my-12">
   
        <div class="w-full xl:w-3/4 lg:w-11/12 flex">
         
          <div
            class="h-auto bg-gray-400 hidden lg:block lg:w-5/12 bg-cover rounded-l-lg"
            style="
              background-image: url('https://cdn.shopify.com/s/files/1/0232/3936/0576/products/Metallicgearssteampunklargeprint_900x.jpg?v=1585249093');
            "
          ></div>
        
          <div class="w-3/4 bg-white p-5 rounded-lg lg:rounded-l-none">
            <div class="headingIn my-auto mt-5 py-10 px-10">
              <h1 class="text-6xl flex justify-center mb-4 font-bold">
                Welcome!
              </h1>
              <h2 class="text-3xl flex justify-center mt-2 mb-8 font-bold">
                Register to acces
              </h2>

              <div class="flex justify-center">
                <form class="w-2/3 flex flex-col" @submit.prevent="signUp">
                  <label
                    class="text-2xl flex font-bold mb-2"
                    for="email"
                    >Email</label>
                  <input
                    class="borderInput"
                    type="text"
                    v-model="email"
                    placeholder="email@gmail.com"
                    id="email"
                    required
                  />
                  <br />
                  <label
                    class="text-2xl flex font-bold mb-2"
                    for="password"
                    >Password</label
                  >
                  <div class="relative w-full">
                    <input
                      class="borderInput mb-6 w-full"
                      :type="passwordFieldType"
                      v-model="password"
                      placeholder="Enter 6 digits password"
                      required
                    /><EyeIcon
                      :class="[passwordFieldIcon]"
                      @click.prevent="hidePassword = !hidePassword"
                      class="eyeColor absolute h-7 w-7 text-blue-300 top-0.5 right-2"
                    />
                    <br />
                  </div>

                  <label
                    class="text-2xl flex font-bold mb-2"
                    for="password"
                    >Confirm password</label
                  >
                  <div  class="relative w-full">
                    <input
                      class="borderInput mb-1 w-full"
                      :type="passwordFieldType"
                      v-model="confirmPassword"
                      placeholder="Confirm 6 digits password"
                      required
                    /><EyeIcon
                      :class="[passwordFieldIcon]"
                      @click.prevent="hidePassword = !hidePassword"
                      class="eyeColor absolute h-7 w-7 text-blue-300 top-0.5 right-2"
                    />
                    <br />
                  </div>

                  <input
                    class="inline-block px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-600 hover:shadow-lg focus:bg-blue-400 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-500 active:shadow-lg transition duration-150 ease-in-out mb-8 mt-8"
                    type="submit"
                    value="Register"
                    required
                  />
                </form>
              </div>
              <div class="text-3xl flex justify-center mb-4 font-bold text-gray-600">
                Check your email
              </div>
              <div class="text-2xl flex justify-center mb-4 font-bold">
                And start organize your tasks todays!
              </div>
              <div class="text-2xl flex justify-center mt-1 font-bold">
                <PersonalRouter :route="route" :buttonText="buttonText" />
              </div>
              <div class="flex justify-around">
                <p align="center" class="flex">
                  <a href="https://www.linkedin.com/in/cescvr/" target="blank"
                    ><img
                      class="m-3"
                      align="center"
                      src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg"
                      alt="CescVila"
                      width="24"
                    />
                  </a>
                  &nbsp;
                  <a href="https://instagram.com/phoenixhawk" target="blank"
                    ><img
                      class="m-3"
                      align="center"
                      src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/instagram.svg"
                      alt="CescVila"
                      width="24"
                    />
                  </a>
                  &nbsp;
                  <a href="https://github.com/CescVila" target="blank"
                    ><img
                      class="m-3"
                      align="center"
                      src="https://pngimg.com/uploads/github/github_PNG40.png"
                      alt="CescVila"
                      width="24"
                    />
                  </a>
                </p>
              </div>
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
import { EyeIcon } from "@heroicons/vue/24/solid";


const route = "/auth/login";
const buttonText = "Click here to Sign In!";


const email = ref("");
const password = ref("");
const confirmPassword = ref("");

const errorMsg = ref("");

const passwordFieldType = computed(() =>
  hidePassword.value ? "password" : "text"
);

const hidePassword = ref(true);

const redirect = useRouter();

const signUp = async () => {
  if (password.value === confirmPassword.value) {
    try {
     
      await useUserStore().signUp(email.value, password.value);
  
      redirect.push({ path: "/auth/login" });
    } catch (error) {
   
      errorMsg.value = error.message;

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
.borderInput {
  border: 3px solid rgb(26, 144, 187);
}
</style>
