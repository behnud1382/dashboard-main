vue
<template>
  <div class="min-h-screen bg-gray-100 py-6 flex flex-col justify-center sm:py-12">
    <div class="relative py-3 sm:max-w-xl sm:mx-auto">
      <div
        class="absolute inset-0 bg-gradient-to-r from-cyan-400 to-sky-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"
      ></div>
      <div class="relative px-4 py-10 bg-white shadow-lg sm:rounded-3xl sm:p-20">
        <div class="max-w-md mx-auto">
          <div>
            <h1 class="text-2xl font-semibold">Sign Up</h1>
          </div>
          <div class="flex items-center justify-between divide-y">
            <h4 class="text-red-600 text-bold">{{ signupMessage }}</h4>
          </div>
          <div class="divide-y divide-gray-200">
            <form @submit.prevent="signup">
              <div class="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
                <div class="relative">
                  <input
                    autocomplete="off"
                    v-model="username"
                    name="username"
                    type="text"
                    class="peer placeholder-transparent h-10 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-rose-600"
                    placeholder="username"
                    required
                  />
                  <label
                    for="username"
                    class="absolute left-0 -top-3.5 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-440 peer-placeholder-shown:top-2 transition-all peer-focus:-top-3.5 peer-focus:text-gray-600 peer-focus:text-sm"
                    >Username</label
                  >
                </div>
                <div class="relative">
                  <input
                    autocomplete="off"
                    v-model="password"
                    placeholder="password"
                    class="peer placeholder-transparent h-10 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-rose-600"
                    type="password"
                    required
                  />
                  <label
                    for="password"
                    class="absolute left-0 -top-3.5 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-440 peer-placeholder-shown:top-2 transition-all peer-focus:-top-3.5 peer-focus:text-gray-600 peer-focus:text-sm"
                    >Password</label
                  >
                </div>
                <div class="relative">
                  <input
                    autocomplete="off"
                    v-model="confirmPassword"
                    placeholder="confirm password"
                    class="peer placeholder-transparent h-10 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-rose-600"
                    type="password"
                    required
                  />
                  <label
                    for="confirm-password"
                    class="absolute left-0 -top-3.5 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-440 peer-placeholder-shown:top-2 transition-all peer-focus:-top-3.5 peer-focus:text-gray-600 peer-focus:text-sm"
                    >Confirm Password</label
                  >
                </div>
                <input
                  class="bg-cyan-500 text-white rounded-md px-2 py-1 hover:bg-cyan-600 transition duration-300"
                  type="submit"
                  value="Sign Up"
                />
              </div>
            </form>
            <div class="w-full flex justify-center">
              <router-link
                to="/login"
                class="bg-blue-500 text-white px-6 py-3 rounded-full hover:bg-blue-600 transition duration-300"
              >
                Already have an account? Log In
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const username = ref('');
const password = ref('');
const confirmPassword = ref('');
const signupMessage = ref('');

// Fetch and sign up user when form is submitted
const signup = async () => {
  const usernameValue = username.value;
  const passwordValue = password.value;
  const confirmPasswordValue = confirmPassword.value;

  if (passwordValue !== confirmPasswordValue) {
    signupMessage.value = "Passwords do not match.";
    return;
  }

  try {
    const res = await fetch('http://localhost:3000/signup', { // Change endpoint to signup
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ username: usernameValue, password: passwordValue })
    });
    const data = await res.json();
    if (res.ok) {
      console.log('User signed up successfully');
      router.push('/login'); // Redirect to login after signup
    } else {
      signupMessage.value = data.message;
    }
  } catch (error) {
    console.error('Error signing up:', error);
  }
};
</script>