<template>
    <form @submit.prevent="submit" class="w-full max-w-md mx-auto mt-8">
        <div class="form-field mb-4">
            <label for="firstName" class="block text-sm font-medium text-gray-700 mb-2">
                First Name
            </label>
            <input 
                id="firstName"
                v-model="state.firstName" 
                type="text"
                placeholder="First Name" 
                class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            />
        </div>
        <button 
            type="submit" 
            class="mt-4 w-full bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-md transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
        >
            Submit
        </button>
    </form>
    <div v-if="response" class="mt-4 p-4 bg-green-100 text-green-800 rounded-md">
        {{ response }}
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const state = ref({
    firstName: ''
})
const response = ref(null)
async function submit() {
    try {
        response.value = await $fetch('/api/contact/test', {
            method: 'post',
            body: { firstName: state.value.firstName }
        })
    } catch (error) {
        alert('Submission failed.')
    }
}
</script>
