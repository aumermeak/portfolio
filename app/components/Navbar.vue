<template>
    <header class="fixed top-0 left-0 w-full z-50">
        <nav class="max-w-6xl mx-auto flex items-center justify-between px-6 py-3 mt-4 
             bg-white/70 backdrop-blur-md shadow-lg rounded-full">
            <!-- Logo -->
            <a href="#hero" class="font-extrabold text-xl text-green-600 tracking-wide hover:scale-105 transition">
                Portfolio
            </a>

            <!-- Desktop Nav -->
            <div class="hidden md:flex space-x-8 font-medium">
                <a href="#about" class="relative text-gray-700 hover:text-green-600 transition duration-200 group">
                    About
                    <span
                        class="absolute left-0 -bottom-1 w-0 h-0.5 bg-green-600 transition-all duration-300 group-hover:w-full"></span>
                </a>
                <a href="#skills" class="relative text-gray-700 hover:text-green-600 transition duration-200 group">
                    Skills
                    <span
                        class="absolute left-0 -bottom-1 w-0 h-0.5 bg-green-600 transition-all duration-300 group-hover:w-full"></span>
                </a>
                <a href="#experience" class="relative text-gray-700 hover:text-green-600 transition duration-200 group">
                    Job Experience
                    <span
                        class="absolute left-0 -bottom-1 w-0 h-0.5 bg-green-600 transition-all duration-300 group-hover:w-full"></span>
                </a>
                <a href="#projects" class="relative text-gray-700 hover:text-green-600 transition duration-200 group">
                    Projects
                    <span
                        class="absolute left-0 -bottom-1 w-0 h-0.5 bg-green-600 transition-all duration-300 group-hover:w-full"></span>
                </a>
                <a href="#contact" class="relative text-gray-700 hover:text-green-600 transition duration-200 group">
                    Contact
                    <span
                        class="absolute left-0 -bottom-1 w-0 h-0.5 bg-green-600 transition-all duration-300 group-hover:w-full"></span>
                </a>
            </div>

            <!-- Desktop CV Button -->
            <div class="hidden md:block">
                <a href="/cv.pdf" download
                    class="px-4 py-2 bg-green-600 text-white rounded-full shadow-md hover:bg-green-700 hover:scale-105 transition">
                    Download CV
                </a>
            </div>

            <!-- Mobile Burger -->
            <button @click="isOpen = !isOpen" class="md:hidden text-gray-700 focus:outline-none">
                <svg v-if="!isOpen" xmlns="http://www.w3.org/2000/svg" class="w-7 h-7" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16" />
                </svg>
                <svg v-else xmlns="http://www.w3.org/2000/svg" class="w-7 h-7" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                </svg>
            </button>
        </nav>

        <!-- Mobile Menu -->
        <transition name="fade">
            <div v-if="isOpen"
                class="md:hidden bg-white/95 backdrop-blur-md shadow-lg rounded-xl mt-2 mx-4 p-4 space-y-4 text-center">
                <a href="#about" class="block text-gray-700 hover:text-green-600">About</a>
                <a href="#skills" class="block text-gray-700 hover:text-green-600">Skills</a>
                <a href="#experience" class="block text-gray-700 hover:text-green-600">Job Experience</a>
                <a href="#projects" class="block text-gray-700 hover:text-green-600">Projects</a>
                <a href="#contact" class="block text-gray-700 hover:text-green-600">Contact</a>
                <a href="/cv.pdf" download
                    class="block px-4 py-2 bg-green-600 text-white rounded-full shadow-md hover:bg-green-700 transition">
                    Download CV
                </a>
            </div>
        </transition>
    </header>
</template>

<script setup>
import { ref } from "vue"
const isOpen = ref(false)
</script>

<style>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>
