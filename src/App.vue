<script setup>
import { ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router'

const sidebarOpen = ref(true)

const toggleSidebar = () => {
  sidebarOpen.value = !sidebarOpen.value
}
</script>

<template>
  <aside :class="{ open: sidebarOpen }">
    <div class="flex items-start gap-2" :class="{ 'justify-end': !sidebarOpen }">
      <img class="h-8" src="https://vuejs.org/images/logo.png" alt="">
      <h1 v-if="sidebarOpen" class="text-xl font-bold">Admin Dash</h1>
    </div>
    <nav class="flex flex-col gap-2 mt-4 border-t border-gray-300 pt-4">
      <RouterLink to="/" active-class="active">
        <i class="fas fa-home"></i>
        <span> Home</span>
      </RouterLink>
      <RouterLink to="/about" active-class="active">
        <i class="fas fa-user"></i>
        <span> About</span>
      </RouterLink>
      <RouterLink to="/contact" active-class="active">
        <i class="fas fa-envelope"></i>
        <span> Contact</span>
      </RouterLink>
      <RouterLink to="/settings" active-class="active">
        <i class="fas fa-cog"></i>
        <span> Settings</span>
      </RouterLink>
    </nav>
  </aside>
  <main :class="{ open: !sidebarOpen }">
    <div class="flex justify-between border-b border-gray-300 p-4 bg-gray-100">
      <button @click="toggleSidebar">
        <i v-if="!sidebarOpen" class=" text-2xl fas fa-toggle-on"></i>
        <i v-else class=" text-2xl fas fa-toggle-off"></i>
      </button>
      <img src="https://vuejs.org/images/logo.png" class="h-8" alt="">
    </div>
    <div class="border p-5 rounded shadow border-gray-300 mb-10 ">
      <router-view v-slot="{ Component, route }">
        <transition :name="route.meta.transition || 'slide-left'" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </div>
  </main>
</template>

<style>
/* tailwind cdn */
@import url('https://cdn.jsdelivr.net/npm/tailwindcss@2.2/dist/tailwind.min.css');
/* fontawesome cdn */
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css');

.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition-duration: 0.3s;
  transition-property: height, opacity, transform;
  transition-timing-function: cubic-bezier(0.55, 0, 0.1, 1);
  overflow: hidden;
}

.slide-left-enter,
.slide-right-leave-active {
  opacity: 0;
  transform: translate(2em, 0);
}

.slide-left-leave-active,
.slide-right-enter {
  opacity: 0;
  transform: translate(-2em, 0);
}

nav a {
  display: block;
  padding: 10px;
  background-color: #fff;
  border-radius: 5px 5px 0 0;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transition: 300ms ease-in-out;
}

nav a.active,
nav a:hover {
  border-bottom: 3px solid #8e00b1;
  color: #8e00b1;
}

aside {
  position: fixed;
  top: 0;
  left: 0;
  width: 200px;
  height: 100vh;
  background-color: #f0f0f0;
  transform: translate(-70%);
  transition: all 300ms ease-in-out;
  padding: 10px;
}

aside.open {
  transform: translate(0);
}

main {
  margin-left: calc(200px);
  transition: all 300ms ease-in-out;
}

main.open {
  margin-left: 60px;
}
</style>