<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
import useAuth from "../composable/useAuth";
import useError from "../composable/useError";


const { isAuthenticated, login, signup, googleLogin } = useAuth();
const username = ref("");
const password = ref("");

const router = useRouter();

const logginIn = async () => {
    await login(username.value, password.value);
    goToHome();
};

const signingUp = async () => {
    await signup(username.value, password.value);
    goToHome();
};

const google = async () => {
    await googleLogin();
    goToHome();
};
const goToHome = () => {
    if (isAuthenticated.value) {
        router.push("/");
    } else {
        setError("Invalid username or password");
        start();
    }
};

const {error, setError } = useError();
import { promiseTimeout, useTimeout } from "@vueuse/core";

const { ready, start } = useTimeout(3000, { controls: true });

</script>




<template>
<div class="flex justify-center flex-col space-y-12 items-center min-h-screen-nonav">
<div class=" bg-gray-300 shadow-2xl justify-center overflow-hidden items-center rounded-lg flex">
<img class="h-64" src="../assets/bglogin.png" alt="Hello BG">
<form @submit.prevent="logginIn" class="flex flex-col space-y-4 p-4">
    <input type="text" class="border-2 p-2 rounded-lg " placeholder="UserName" v-model="username" />
    <input type="password" class="border-2 p-2 rounded-lg" placeholder="Password" v-model="password" />

    <div class="flex space-x-2">
    <button type="submit" @submit.prevent="logginIn" class="bg-pink-500 rounded-lg w-1/2 text-gray-800 py-2">Login</button>

    <button  @click="signingUp" class="bg-green-800 rounded-lg w-1/2 text-yellow-400 py-2">Signup</button>
    </div>

<button 
    @click="google"
    class="bg-white flex justify-center py-2 rounded-lg hover:bg-green-400"> 
    <img src="https://upload.wikimedia.org/wikipedia/commons/5/53/Google_%22G%22_Logo.svg"></button>
</form>
</div>
<div
v-if="!ready && error"
 class="bg-red-300  w-1/4 p-4 text-red-800 rounded-lg absolute bottom-2 right-2 text-center">
    {{error}}
</div>
</div>
</template>