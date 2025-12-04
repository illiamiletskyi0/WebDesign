<template>
  <div
    class="max-w-[414px] w-full mx-auto h-[90vh] bg-[#FF5F5F] flex items-center justify-center p-6"
  >
    <div class="w-full max-w-sm rounded-2xl p-10">
      <div class="text-center mb-6">
        <img
          src="../img/pngwing.com.png"
          alt="heart"
          class="w-40 h-40 mx-auto mb-4 object-contain"
        />
        <div
          class="text-white text-4xl font-extrabold tracking-widest uppercase"
          style="font-family: 'Cherry Bomb One', cursive"
        >
          FATED
        </div>
      </div>

      <div class="flex gap-4 mb-6">
        <button
          @click="mode = 'login'"
          :class="[
            'flex-1 py-3 text-sm font-semibold uppercase rounded-md transition-all duration-300 ease-in-out transform',
            mode === 'login'
              ? 'bg-white text-[#FF5F5F] shadow-lg scale-105'
              : 'text-white bg-transparent hover:bg-[rgba(255,255,255,0.1)] hover:scale-102',
          ]"
        >
          Login
        </button>
        <button
          @click="mode = 'register'"
          :class="[
            'flex-1 py-3 text-sm font-semibold uppercase rounded-md transition-all duration-300 ease-in-out transform',
            mode === 'register'
              ? 'bg-white text-[#FF5F5F] shadow-lg scale-105'
              : 'text-white bg-transparent hover:bg-[rgba(255,255,255,0.1)] hover:scale-102',
          ]"
        >
          Register
        </button>
      </div>

      <transition name="form-fade" mode="out-in">
        <div :key="mode">
          <form v-if="mode === 'login'" @submit.prevent="handleLogin" class="space-y-4">
            <div>
              <input
                v-model="loginForm.username"
                type="text"
                class="w-full p-4 rounded-md bg-white text-gray-800 placeholder-gray-400 text-center focus:outline-none focus:ring-2 focus:ring-[#FF5F5F]"
                placeholder="user name"
                minlength="3"
                required
              />
              <p v-if="loginErrors.username" class="text-white text-xs mt-1">
                {{ loginErrors.username }}
              </p>
            </div>

            <div>
              <input
                v-model="loginForm.password"
                type="password"
                class="w-full p-4 rounded-md bg-white text-gray-800 placeholder-gray-400 text-center focus:outline-none focus:ring-2 focus:ring-[#FF5F5F]"
                placeholder="password"
                minlength="6"
                required
              />
              <p v-if="loginErrors.password" class="text-white text-xs mt-1">
                {{ loginErrors.password }}
              </p>
            </div>

            <div class="text-right -mt-2 mb-2">
              <a href="#" class="text-white text-xs uppercase tracking-wide hover:underline"
                >Forgot Password?</a
              >
            </div>

            <button
              type="submit"
              class="w-full py-4 rounded-md bg-white text-[#FF5F5F] font-bold uppercase tracking-wider shadow hover:shadow-lg transition-shadow"
            >
              LOGIN
            </button>

            <div class="text-center text-white text-xs uppercase tracking-wide mt-2">
              DON'T HAVE AN ACCOUNT?
              <button
                @click.prevent="mode = 'register'"
                class="font-bold underline hover:no-underline"
              >
                REGISTER
              </button>
            </div>
          </form>

          <form v-if="mode === 'register'" @submit.prevent="handleRegister" class="space-y-4">
            <div>
              <input
                v-model="registerForm.username"
                type="text"
                class="w-full p-4 rounded-md bg-white text-gray-800 placeholder-gray-400 text-center focus:outline-none focus:ring-2 focus:ring-[#FF5F5F]"
                placeholder="user name"
                minlength="3"
                required
              />
              <p v-if="registerErrors.username" class="text-white text-xs mt-1">
                {{ registerErrors.username }}
              </p>
            </div>

            <div>
              <input
                v-model="registerForm.email"
                type="email"
                class="w-full p-4 rounded-md bg-white text-gray-800 placeholder-gray-400 text-center focus:outline-none focus:ring-2 focus:ring-[#FF5F5F]"
                placeholder="email"
                required
              />
              <p v-if="registerErrors.email" class="text-white text-xs mt-1">
                {{ registerErrors.email }}
              </p>
            </div>

            <div>
              <input
                v-model="registerForm.password"
                type="password"
                class="w-full p-4 rounded-md bg-white text-gray-800 placeholder-gray-400 text-center focus:outline-none focus:ring-2 focus:ring-[#FF5F5F]"
                placeholder="password"
                minlength="6"
                required
              />
              <p v-if="registerErrors.password" class="text-white text-xs mt-1">
                {{ registerErrors.password }}
              </p>
            </div>

            <div class="text-right -mt-2 mb-2">
              <a href="#" class="text-white text-xs uppercase tracking-wide hover:underline"
                >Forgot Password?</a
              >
            </div>

            <button
              type="submit"
              class="w-full py-4 rounded-md bg-white text-[#FF5F5F] font-bold uppercase tracking-wider shadow hover:shadow-lg transition-shadow"
            >
              Register
            </button>

            <div class="text-center text-white text-xs uppercase tracking-wide mt-2">
              Already have an account?
              <button
                @click.prevent="mode = 'login'"
                class="font-bold underline hover:no-underline"
              >
                Login
              </button>
            </div>
          </form>
        </div>
      </transition>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const mode = ref<'login' | 'register'>('login')

const loginForm = ref({
  username: '',
  password: '',
})

const registerForm = ref({
  username: '',
  email: '',
  password: '',
})

const loginErrors = ref({
  username: '',
  password: '',
})

const registerErrors = ref({
  username: '',
  email: '',
  password: '',
})

const showValidationError = ref(false)

function validateLogin(): boolean {
  loginErrors.value = { username: '', password: '' }
  showValidationError.value = false
  let isValid = true

  if (loginForm.value.username.length < 3) {
    loginErrors.value.username = 'Username must be at least 3 characters'
    isValid = false
  }

  if (loginForm.value.password.length < 6) {
    loginErrors.value.password = 'Password must be at least 6 characters'
    isValid = false
  }

  if (!isValid) {
    showValidationError.value = true
  }

  return isValid
}

function validateRegister(): boolean {
  registerErrors.value = { username: '', email: '', password: '' }
  showValidationError.value = false
  let isValid = true

  if (registerForm.value.username.length < 3) {
    registerErrors.value.username = 'Username must be at least 3 characters'
    isValid = false
  }

  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!emailRegex.test(registerForm.value.email)) {
    registerErrors.value.email = 'Please enter a valid email'
    isValid = false
  }

  if (registerForm.value.password.length < 6) {
    registerErrors.value.password = 'Password must be at least 6 characters'
    isValid = false
  }

  if (!isValid) {
    showValidationError.value = true
  }

  return isValid
}

function handleLogin() {
  if (validateLogin()) {
    console.log(`Username: ${loginForm.value.username}\nPassword: ${loginForm.value.password}`)
  }
}

function handleRegister() {
  if (validateRegister()) {
    console.log(
      `Username: ${registerForm.value.username}\nEmail: ${registerForm.value.email}\nPassword: ${registerForm.value.password}`,
    )
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cherry+Bomb+One&display=swap');

.form-fade-enter-active,
.form-fade-leave-active {
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.form-fade-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

.form-fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

button {
  will-change: transform;
}

button:active {
  transform: scale(0.98);
}
</style>
