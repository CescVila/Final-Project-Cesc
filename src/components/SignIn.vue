<template>
  <!-- <div class="containerIn">
    <div class="headingIn m-auto mt-20 w-3/5 py-10 px-40 w-">
      <h1 class="text-6xl flex justify-center mb-5">Welcome to Task App</h1>
      <h2 class="text-3xl flex justify-center mt-2 mb-14">Start Organizing your tasks today!</h2>

      <div>
        <form @submit.prevent="signIn" class="mt-5 flex flex-col px-56">
          <label for="email" class="flex justify-center">Email</label>
          <input
            class="mt-2 mb-5"
            type="text"
            v-model="email"
            placeholder="email@gmail.com"
            required
          />
          <label for="password"  class="flex justify-center">Password</label>
          <input
            class="mt-2 mb-5"
            type="password"
            v-model="password"
            placeholder="******"
            required
          />
          <br />
          <input
            class="inline-block px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-600 hover:shadow-lg focus:bg-blue-400 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-500 active:shadow-lg transition duration-150 ease-in-out mb-10"
            type="submit"
            required
          />
        </form>
        
      </div>

      <div class="text-2xl flex justify-center mb-4">Start Organizing your tasks todays!</div>
      <div class="text-2xl flex justify-center mt-3"><PersonalRouter :route="route" :buttonText="buttonText" /></div>
    </div>

    <div class="img">
      <img
        src="https://www.impressline.com.mx/public/uploads/productos/ESC-543t.jpg"
        alt=""
      />
    </div>
  </div>
 -->

  <div>
    <!-- Container -->
    <div>
      <div class="flex justify-center px-6 my-12">
        <!-- Row -->
        <div class="w-full xl:w-3/4 lg:w-11/12 flex">
          <!-- Col -->
          <div
            class="h-auto bg-gray-400 hidden md:block md:w-5/12 bg-cover rounded-l-lg"
            style="
              background-image: url('https://blog.omysa.com/wp-content/uploads/2020/03/Home-Office-Plant-scaled.jpg');
            "
          ></div>
          <!-- Col -->
          <div
            class="w-full lg:w-7/12 bg-white p-5 rounded-lg lg:rounded-l-none"
          >
            <div class="headingIn m-auto mt-5 w-3/5 py-10 px-10">
              <h1 class="text-center text-6xl font-bold flex justify-center mb-5">
                Welcome to Task App
              </h1>
              
              <div>
                <form @submit.prevent="signIn" class="mt-5 flex flex-col">
                  <label for="email" class="text-2xl font-bold flex justify-center">Email</label>
                  <input
                    class="mt-2 mb-5 borderInput"
                    type="text"
                    v-model="email"
                    placeholder="email@gmail.com"
                    required
                  />
                  <label for="password" class="text-2xl font-bold flex justify-center"
                    >Password</label
                  >
                  <input
                    class="mt-2 mb-5 borderInput"
                    type="password"
                    v-model="password"
                    placeholder="******"
                    required
                  />
                  <br />
                  <input
                    class="inline-block px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-600 hover:shadow-lg focus:bg-blue-400 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-500 active:shadow-lg transition duration-150 ease-in-out mb-10"
                    type="submit"
                    required
                  />
                </form>
              </div>

              <div class="text-2xl flex justify-center mb-4 font-bold">
                Organize your tasks todays!
              </div>
              <div class="text-2xl flex justify-center mt-3 mb-3 font-bold">
                <PersonalRouter :route="route" :buttonText="buttonText" />
              </div>

              <div class="flex justify-around">
                <p align="center" class="flex ">
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
import { ref, computed } from "vue";
import PersonalRouter from "./PersonalRouter.vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";

// Route Variables
const route = "/auth/sign-up";
const buttonText = "Click here to register!";

// Input Fields
const email = ref("");
const password = ref("");

// Error Message
const errorMsg = ref("");

//Show hide password variables
const passwordFieldType = computed(() =>
  hidePassword.value ? "password" : "text"
);
const hidePassword = ref(true);

// Router to push user once SignedIn to the HomeView
const redirect = useRouter();

// Arrow function to Signin user to supaBase
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
.wu-text {
  color: black;
}

.form {
  display: flex;
  flex-direction: column;
  margin: 1rem 0;
}
.input {
  color: black;
  margin-bottom: 1rem;
}
.button {
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 10px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
.containerIn {
  display: flex;
  flex-direction: row;
  background-image: url(con);
}
.headingIn {
  margin-top: 100px;
}
.borderInput {
  border: 3px solid rgb(26, 144, 187);
}
</style>
