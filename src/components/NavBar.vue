<template>
    <nav class="bg-amber-600 p-4 shadow-md">
      <div class="container mx-auto flex justify-between items-center">
        
        <div class="text-white text-xl font-bold">
          <router-link to="/" class="hover:text-amber-900"> Movie Gallery</router-link>
        </div>
        
        <div class="hidden md:flex space-x-4">
          <router-link to="/" class="text-white hover:text-amber-900">Home</router-link>
          <router-link to="/about" class="text-white hover:text-amber-900">About</router-link>
        </div>
        
        <button @click="toggleMenu" class="text-white md:hidden">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path>
          </svg>
        </button>
      </div>
      
      <div v-if="isMenuOpen" class="md:hidden mt-4">
        <router-link to="/" class="block text-white hover:text-amber-900 py-2">Home</router-link>
        <router-link to="/about" class="block text-white hover:text-amber-900 py-2">About</router-link>
      </div>
    </nav>
  </template>
  
  <script>
  export default {
    name: 'NavBar',
    data() {
      return {
        isMenuOpen: false,
      };
    },
    methods: {
      toggleMenu() {
        this.isMenuOpen = !this.isMenuOpen;
      },
    },
  };
  </script>
  
  <style scoped>
 
  </style>
  