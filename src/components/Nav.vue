<script setup>
import {useRouter} from "vue-router";
import useAuth from "../composable/useAuth";
const {isAuthenticated, logout} = useAuth();

const router = useRouter();

const loggingOut = () => {
    logout();
    router.push("/");
}

</script>




<template>
   <div class="bg-green-800 text-yellow-300">
        <div class="container mx-auto flex items-center italic justify-between ">
            <h1 class="tracking-tighter text-3xl font-semibold">
                Vue<span class="font-normal">RealAuth</span>
                </h1>
            <nav>
                <ul class="flex space-x-4">
                    <router-link to="/">
                    <li class="py-8 px-4  hover:cursor-pointer hover:bg-yellow-300 hover:text-green-800">
                        Home
                        </li></router-link>
                     <router-link to="/about">   
                    <li class="py-8 px-4 hover:cursor-pointer hover:bg-yellow-300 hover:text-green-800">About</li>
                    </router-link>
                    <router-link v-if="!isAuthenticated" to="/login">
                    <li class="py-8 px-4 hover:cursor-pointer hover:bg-yellow-300 hover:text-green-800">Login</li>
                    </router-link>

                    <div v-else class="flex">
                     <router-link  to="/secret">
                    <li class="py-8 px-4 hover:cursor-pointer hover:bg-yellow-300 hover:text-green-800">Secret</li>
                    </router-link>


                     <button  @click="loggingOut">
                    <li class="py-8 px-4 hover:cursor-pointer hover:bg-yellow-300 hover:text-green-800">Logout</li>
                    </button>
                    </div>
                    
                </ul>

            </nav>
        </div>
        </div>
    
</template>