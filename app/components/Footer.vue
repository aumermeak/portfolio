<template>
    <footer class="bg-gray-800 text-gray-200 py-10">
        <div class="max-w-6xl mx-auto px-6 flex flex-col md:flex-row justify-between items-center gap-6">

            <div class="text-center md:text-left">
                <h1 class="text-2xl font-bold text-green-500 mb-2">Aumer Meak Bagorio</h1>
                <p class="text-gray-400 text-sm">Building seamless web experiences & gaming vibes 🎮</p>
            </div>

            <div class="flex flex-col md:flex-row gap-6 text-center md:text-left">
                <a href="#about" class="hover:text-green-500 transition">About</a>
                <a href="#skills" class="hover:text-green-500 transition">Skills</a>
                <a href="#experience" class="hover:text-green-500 transition">Job Experience</a>
                <a href="#projects" class="hover:text-green-500 transition">Projects</a>
                <a href="#contact" class="hover:text-green-500 transition">Contact</a>
            </div>

            <div class="flex gap-4">
                <a href="https://github.com/aumermeak" target="_blank" class="bg-green-600 p-2 rounded-full hover:bg-green-700 transition">
                    <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg"
                        class="w-6 h-6" alt="GitHub" />
                </a>
                <a href="https://www.linkedin.com/in/aumer-meak-bagorio-1117a8317/" target="_blank"
                    class="bg-green-600 p-2 rounded-full hover:bg-green-700 transition">
                    <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linkedin/linkedin-original.svg"
                        class="w-6 h-6" alt="LinkedIn" />
                </a>
                <a href="https://ph.jobstreet.com/profile/aumermeak-bagorio-4HQ3Q07lJ7" target="_blank"
                    class="bg-green-600 p-2 rounded-full hover:bg-green-700 transition">
                    <img src="https://cdn.brandfetch.io/idHY-qDocV/w/60/h/60/theme/dark/logo.png?c=1dxbfHSJFAPEGdCLU4o5B"
                        class="w-6 h-6" alt="JobStreet" />
                </a>
            </div>

        </div>

       
        <div class="mt-8 border-t border-gray-700 pt-4 text-center text-gray-500 text-sm">
            &copy; {{ new Date().getFullYear() }} Aumer Meak Bagorio. All rights reserved.
        </div>
    </footer>
</template>