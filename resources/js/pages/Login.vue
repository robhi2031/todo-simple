<template>
    <div class="relative flex flex-col justify-center min-h-screen overflow-hidden">
        <div
            class="w-full p-6 m-auto bg-white border-t-4 border-purple-600 rounded-md shadow-md border-top lg:max-w-md">
            <h1 class="text-3xl font-semibold text-center text-purple-700">TODO SIMPLE</h1>
            <h3 class="text-2xl font-semibold text-center">LOGIN</h3>
            <!-- eslint-disable vue/no-use-v-if-with-v-for,vue/no-confusing-v-for-v-if -->
            <ul class="list-outside hover:list-inside" v-for="(value, index) in errors" :key="index"
                v-if="typeof errors === 'object'">
                <li>{{ value[0] }}</li>
            </ul>
            <p class="text-red-500 text-center" v-if="typeof errors === 'string'">{{ errors }}</p>
            <form class="mt-6" method="post" @submit.prevent="handleLogin">
                <div>
                    <label for="username" class="block text-sm text-gray-800">Email</label>
                    <input type="email" id="username" v-model="form.email" required
                        class="block w-full px-4 py-2 mt-2 text-purple-700 bg-white border rounded-md focus:border-purple-400 focus:ring-purple-300 focus:outline-none focus:ring focus:ring-opacity-40">
                </div>
                <div class="mt-4">
                    <div>
                        <label for="password" class="block text-sm text-gray-800">Password</label>
                        <input id="password" type="password" v-model="form.password" required
                            class="block w-full px-4 py-2 mt-2 text-purple-700 bg-white border rounded-md focus:border-purple-400 focus:ring-purple-300 focus:outline-none focus:ring focus:ring-opacity-40">
                    </div>
                </div>
                <a href="#" class="text-xs text-gray-600 hover:underline">Forget Password?</a>
                <div class="mt-6">
                    <button type="submit"
                        class="w-full px-4 py-2 tracking-wide text-white transition-colors duration-200 transform bg-purple-700 rounded-md hover:bg-purple-600 focus:outline-none focus:bg-purple-600">
                        Login
                    </button>
                </div>
            </form>
            <p class="mt-8 text-xs font-light text-center text-gray-700"> Don't have an account? <router-link
                    to="register" class="font-medium text-purple-600 hover:underline">Sign up</router-link></p>
        </div>
    </div>
</template>

<script>
import { reactive, ref } from 'vue';
import axios from 'axios';
import { useRouter } from "vue-router";
export default {
    setup() {
        const errors = ref()
        const router = useRouter();
        const form = reactive({
            email: '',
            password: '',
        })
        const handleLogin = async () => {
            try {
                const result = await axios.post('/api/auth/login', form)
                if (result.status === 200 && result.data && result.data.token) {
                    localStorage.setItem('APP_DEMO_USER_TOKEN', result.data.token)
                    await router.push('home')
                }
            } catch (e) {
                if (e && e.response.data && e.response.data.errors) {
                    errors.value = Object.values(e.response.data.errors)
                } else {
                    errors.value = e.response.data.message || ""
                }
            }
        }

        return {
            form,
            errors,
            handleLogin,
        }
    }
}
</script>