<script setup>
import { reactive } from 'vue';
import { router } from '@inertiajs/vue3';
import { useForm }from '@inertiajs/vue3';
import TextInput from '../Components/TextInput.vue';

const form = useForm({
    name: null,
    email: null,
    password: null,
    password_confirmation: null
})

const submit = () => {
    // router.post('/register', form)
    form.post('/register', {
        onError: () => {
            form.reset('password', 'password_confirmation')
        }
    })
}
</script>

<template>

    <Head title="| Register" />
    <h1 class="title">Register a new account</h1>

    <div class="w-2/4 mx-auto">
        <form @submit.prevent="submit">
            <TextInput 
                name="name" 
                v-model="form.name" 
                :message="form.errors.name" 
            />

            <TextInput 
                name="email"
                type="email" 
                v-model="form.email" 
                :message="form.errors.email" 
            />

            <TextInput 
                name="password" 
                type="password"
                v-model="form.password" 
                :message="form.errors.password" 
            />

            <TextInput 
                name="confirm password" 
                type="password"
                v-model="form.password_confirmation" 
            />
            <div class="mt-6 flex items-center justify-between">
                <p class="text-slate-600">
                    Already a user?
                    <Link :href="route('login')" class="text-blue-600 hover:text-blue-800 hover:underline ml-1">
                        Login
                    </Link>
                </p>
                <button
                    class="primary-btn bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
                    Register
                </button>
            </div>
        </form>
    </div>
</template>