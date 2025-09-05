<script setup lang="ts">
import { ref, onMounted, onUnmounted, watch } from "vue"

// existing refs
const showButton = ref(false)
const showModal = ref(false)
const sections = ref<NodeListOf<Element> | null>(null)

const skills = ref([
    { name: "Front-end Development", points: 85, current: 0 },
    { name: "Design", points: 80, current: 0 },
    { name: "Back-end Development", points: 30, current: 0 },
    { name: "Linux (Ubuntu)", points: 40, current: 0 },
    { name: "Front-End To Back-End API Integration", points: 70, current: 0 },
])

// typing effect
const fullText = "want to collaborate, or just communicate."
const displayText = ref<string>("")
const isDeleting = ref<boolean>(false)
let i = 0
let speed = 100

function typeEffect(): void {
    if (!isDeleting.value) {
        if (i < fullText.length) {
            displayText.value += fullText[i]
            i++
            setTimeout(typeEffect, speed)
        } else {
            setTimeout(() => {
                isDeleting.value = true
                typeEffect()
            }, 2000)
        }
    } else {
        if (i > 0) {
            displayText.value = fullText.substring(0, i - 1)
            i--
            setTimeout(typeEffect, speed / 2)
        } else {
            isDeleting.value = false
            setTimeout(typeEffect, speed)
        }
    }
}

// scroll button logic
const handleScroll = () => {
    showButton.value = window.scrollY > 200 // instead of 200
}

// skill animation
watch(showModal, (newVal) => {
    if (newVal) {
        skills.value.forEach((skill) => (skill.current = 0))
        setTimeout(() => {
            skills.value.forEach((skill) => {
                skill.current = skill.points
            })
        }, 200)
    }
})

const scrollToTop = () => {
    window.scrollTo({ top: 0, behavior: "smooth" })
}

onMounted(() => {
    window.addEventListener("scroll", handleScroll)
    typeEffect() // start typing effect
})

onUnmounted(() => {
    window.removeEventListener("scroll", handleScroll)
})

onMounted(() => {
    sections.value = document.querySelectorAll(".fade-in-section")

    const observer = new IntersectionObserver(
        (entries) => {
            entries.forEach((entry) => {
                if (entry.isIntersecting) {
                    entry.target.classList.add("opacity-100", "translate-y-0")
                    entry.target.classList.remove("opacity-0", "translate-y-10")
                }
            })
        },
        { threshold: 0.1 }
    )

    sections.value.forEach((section) => observer.observe(section))
})
</script>




<template>
    <div class="font-sans text-gray-900 scroll-smooth">

        <Navbar />


        <section id="hero" class="min-h-screen flex flex-col items-center justify-center text-center px-6">
            <img src="/gradpic.jpg" alt="My photo" class="w-60 h-60 rounded-full shadow-lg mb-6 border-4 border-green-500 cursor-pointer 
         hover:shadow-2xl transition duration-300 hover:float-animation" @click="showModal = true" />
            <h1 class="text-5xl md:text-6xl font-bold mb-4">
                Hi, I’m <span class="text-green-500">Aumer Meak Bagorio</span>
            </h1>
            <p class="text-lg md:text-xl text-gray-600 mb-6 max-w-xl">
                Frontend Developer • IT • Gaming Enthusiast 🎮
            </p>
            <div class="flex justify-center md:justify-start gap-4">
                <button @click="showModal = true"
                    class="px-6 py-3 bg-gray-200 text-gray-800 rounded-lg shadow hover:bg-gray-300 transition cursor-pointer">
                    My Skills & Stack
                </button>

                <a href="/Aumer-Meak-G.pdf" download
                    class="px-4 py-2 bg-gray-800 text-white rounded-lg shadow hover:bg-gray-900 transition">
                    Download CV
                </a>
            </div>
        </section>


        <section id="about"
            class="py-20 px-6 bg-gray-50 fade-in-section opacity-0 translate-y-10 transition-all duration-700">
            <div class="max-w-3xl mx-auto text-center">
                <h2 class="text-3xl font-bold mb-6">About Me</h2>
                <p class="text-gray-600 leading-relaxed">
                    I’m a passionate frontend developer who loves creating seamless, responsive, and modern web
                    experiences.
                    When I’m not coding, you can find me sitting in front of my computer playing games or watching
                    movies or experimenting with new tech.
                </p>
            </div>
        </section>


        <section id="skills"
            class="py-20 px-6 bg-white fade-in-section opacity-0 translate-y-10 transition-all duration-700">
            <div class="max-w-5xl mx-auto text-center">
                <h2 class="text-3xl font-bold mb-8 text-gray-900">My Skills & Stacks</h2>
                <p class="text-gray-600 mb-12">Technologies, stacks, and tools I work with 🚀</p>


                <div class="space-y-8 text-left mb-16">

                    <div>
                        <div class="flex justify-between mb-2">
                            <span class="font-medium text-gray-800">Front-End Development</span>
                            <span class="text-gray-600">85%</span>
                        </div>
                        <div class="w-full bg-gray-200 rounded-full h-3">
                            <div class="bg-green-600 h-3 rounded-full" style="width: 85%"></div>
                        </div>
                    </div>


                    <div>
                        <div class="flex justify-between mb-2">
                            <span class="font-medium text-gray-800">Design</span>
                            <span class="text-gray-600">80%</span>
                        </div>
                        <div class="w-full bg-gray-200 rounded-full h-3">
                            <div class="bg-green-600 h-3 rounded-full" style="width: 80%"></div>
                        </div>
                    </div>
                    <div>
                        <div class="flex justify-between mb-2">
                            <span class="font-medium text-gray-800">Back-End Development</span>
                            <span class="text-gray-600">30%</span>
                        </div>
                        <div class="w-full bg-gray-200 rounded-full h-3">
                            <div class="bg-green-600 h-3 rounded-full" style="width: 30%"></div>
                        </div>
                    </div>

                    <div>
                        <div class="flex justify-between mb-2">
                            <span class="font-medium text-gray-800">Linux (Ubuntu)</span>
                            <span class="text-gray-600">40%</span>
                        </div>
                        <div class="w-full bg-gray-200 rounded-full h-3">
                            <div class="bg-green-600 h-3 rounded-full" style="width: 40%"></div>
                        </div>
                    </div>


                    <div>
                        <div class="flex justify-between mb-2">
                            <span class="font-medium text-gray-800">Front-End To Back-End API Integration</span>
                            <span class="text-gray-600">70%</span>
                        </div>
                        <div class="w-full bg-gray-200 rounded-full h-3">
                            <div class="bg-green-600 h-3 rounded-full" style="width: 70%"></div>
                        </div>
                    </div>
                </div>


                <div>
                    <h3 class="text-xl font-semibold mb-6 text-green-600">Languages, Stacks & Tools</h3>
                    <div class="flex flex-wrap justify-center gap-8">

                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="HTML" />
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="CSS" />
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="JavaScript" />
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="TypeScript" />
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/php/php-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="PHP" />
                        <img src="https://flowbite.s3.amazonaws.com/logo.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="Flowbite" />
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuetify/vuetify-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="Vuetify" />


                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="Vue.js" />
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nuxtjs/nuxtjs-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="Nuxt.js" />
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/laravel/laravel-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="Laravel" />
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="TailwindCSS" />


                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="Figma" />
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="GitHub" />
                        <img src="https://www.vectorlogo.zone/logos/getpostman/getpostman-icon.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="Postman" />
                        <img src="https://raw.githubusercontent.com/get-icon/geticon/master/icons/insomnia.svg"
                            class="w-14 h-14 hover:scale-110 transition" alt="Insomnia" />
                    </div>
                </div>
            </div>
        </section>

        <section id="experience"
            class="py-20 px-6 fade-in-section opacity-0 translate-y-10 transition-all duration-700">
            <div class="max-w-5xl mx-auto">
                <h2 class="text-3xl font-bold mb-8 text-center">Job Experience</h2>

                <div class="space-y-8">

                    <div class="p-6 bg-white shadow rounded-xl border-l-4 border-green-500">
                        <h3 class="text-xl font-semibold text-gray-900">Project-Based Frontend Developer</h3>
                        <p class="text-gray-600 text-sm mb-2">Seaversity • Aug 2023 – July 2024</p>
                        <ul class="list-disc list-inside text-gray-700">
                            <li>Developed responsive web applications using Vue, Nuxt, and TailwindCSS.</li>
                            <li>Collaborated with designers to implement modern UI/UX features.</li>
                            <li>Collaborated with Back-End Developers to connect Front-end to Back-End</li>
                            <li>Optimized applications for performance and scalability.</li>
                        </ul>
                    </div>


                    <div class="p-6 bg-white shadow rounded-xl border-l-4 border-green-500">
                        <h3 class="text-xl font-semibold text-gray-900">Internship</h3>
                        <p class="text-gray-600 text-sm mb-2">Seaversity • March 2023 – July 2023</p>
                        <ul class="list-disc list-inside text-gray-700">
                            <li>Assisted in developing internal tools using HTML, CSS, and JavaScript.</li>
                            <li>Learned agile workflows and team collaboration.</li>
                            <li>Created documentation for system processes.</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>
        <section id="projects"
            class="py-20 px-6 bg-gray-50 fade-in-section opacity-0 translate-y-10 transition-all duration-700">
            <div class="max-w-5xl mx-auto">
                <h2 class="text-3xl font-bold mb-8 text-center">Projects & Contributions</h2>

                <div class="grid md:grid-cols-2 gap-8">

                    <div class="p-6 bg-white shadow rounded-xl hover:shadow-lg transition border-t-4 border-green-500">
                        <h3 class="text-xl font-semibold text-gray-900">Inventory Management System</h3>
                        <p class="text-gray-600 text-sm mb-3">Seaversity • Aug 2023 – Dec 2024</p>
                        <ul class="list-disc list-inside text-gray-700 space-y-1">
                            <li>Built responsive web pages using Vue, Nuxt, and TailwindCSS.</li>
                            <li>Implemented user friendly design</li>
                            <li>Collaborated with backend team for API integrations.</li>
                        </ul>
                    </div>


                    <div class="p-6 bg-white shadow rounded-xl hover:shadow-lg transition border-t-4 border-green-500">
                        <h3 class="text-xl font-semibold text-gray-900">Academic Management System</h3>
                        <p class="text-gray-600 text-sm mb-3">Seaversity • March 2025 – July 2025</p>
                        <ul class="list-disc list-inside text-gray-700 space-y-1">
                            <li>Built responsive web pages using Vue, Nuxt, and TailwindCSS.</li>
                            <li>Collaborated with other team members for coding review.</li>
                            <li>Collaborated with backend team for API integrations.</li>
                        </ul>
                    </div>
                    <div class="p-6 bg-white shadow rounded-xl hover:shadow-lg transition border-t-4 border-green-500">
                        <h3 class="text-xl font-semibold text-gray-900">Campus Food Ordering System (CFOS)</h3>
                        <p class="text-gray-600 text-sm mb-3">Technological University Of The Philippines - Manila
                            (Thesis) • 2022 – 2023</p>
                        <ul class="list-disc list-inside text-gray-700 space-y-1">
                            <li>Built responsive web pages using native PHP.</li>
                            <li>Helped create complex function such as timer and open and close time of each store</li>
                            <li>Helped optimize existing code for maintainability.</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section id="contact"
            class="py-20 px-6 bg-gradient-to-b from-gray-50 to-white fade-in-section opacity-0 translate-y-10 transition-all duration-700">
            <div class="max-w-5xl mx-auto">
                <h2 class="text-3xl font-bold text-center mb-12 text-gray-800"> Contact Me</h2>

                <div
                    class="bg-white shadow-xl rounded-2xl p-10 md:grid md:grid-cols-2 gap-10 items-center hover:shadow-2xl transition">

                    <!-- Left Column (Image + Intro) -->
                    <div class="flex flex-col items-center text-center justify-center h-full space-y-4">
                        <img src="/gradpic.jpg" alt="Your Photo"
                            class="w-36 h-36 object-cover rounded-full border-4 border-green-500 shadow-lg" />

                        <h3 class="text-xl font-bold text-gray-800">Aumer Meak Bagorio</h3>
                        <p class="text-green-600 font-medium">Front-End Web Developer</p>

                        <div class="max-w-xl">
                            <p class="text-gray-600 leading-relaxed break-words">
                                Always happy to connect — whether it’s to discuss a project idea,
                                <span>{{ displayText }}</span><span class="cursor"></span>
                            </p>
                        </div>
                    </div>

                    <!-- Right Column (Contact Info) -->
                    <div class="space-y-6">
                        <!-- Phone -->
                        <div class="flex items-center gap-3">
                            <div class="bg-green-100 text-green-600 p-3 rounded-full">📞</div>
                            <div>
                                <p class="font-semibold text-gray-700">Phone</p>
                                <p class="text-gray-800">+63 943 553 3691</p>
                            </div>
                        </div>

                        <!-- Email -->
                        <div class="flex items-center gap-3">
                            <div class="bg-green-100 text-green-600 p-3 rounded-full">✉️</div>
                            <div>
                                <p class="font-semibold text-gray-700">Email</p>
                                <p class="text-gray-800 break-all">aumermeakgloriabagorio@gmail.com</p>
                            </div>
                        </div>

                        <!-- Location -->
                        <div class="flex items-center gap-3">
                            <div class="bg-green-100 text-green-600 p-3 rounded-full">📍</div>
                            <div>
                                <p class="font-semibold text-gray-700">Location</p>
                                <p class="text-gray-800">Valenzuela City</p>
                            </div>
                        </div>

                        <!-- Social Icons -->
                        <div class="flex justify-center md:justify-start gap-4 mt-6">
                            <a href="https://github.com/aumermeak" target="_blank"
                                class="bg-green-600 p-3 rounded-full inline-flex items-center justify-center hover:bg-green-700 transition">
                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg"
                                    class="w-6 h-6" alt="GitHub" />
                            </a>

                            <a href="https://www.linkedin.com/in/aumer-meak-bagorio-1117a8317/" target="_blank"
                                class="bg-green-600 p-3 rounded-full inline-flex items-center justify-center hover:bg-green-700 transition">
                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linkedin/linkedin-original.svg"
                                    class="w-6 h-6" alt="LinkedIn" />
                            </a>

                            <a href="https://ph.jobstreet.com/profile/aumermeak-bagorio-4HQ3Q07lJ7" target="_blank"
                                class="bg-green-600 p-3 rounded-full inline-flex items-center justify-center hover:bg-green-700 transition">
                                <img src="https://cdn.brandfetch.io/idHY-qDocV/w/60/h/60/theme/dark/logo.png?c=1dxbfHSJFAPEGdCLU4o5B"
                                    class="w-6 h-6" alt="JobStreet" />
                            </a>
                        </div>
                    </div>
                </div>
            </div>


        </section>
        <!-- Back to Top Button -->
        <button v-show="showButton" @click="scrollToTop" class="fixed bottom-6 right-6 w-12 h-12 flex items-center justify-center rounded-full 
           bg-gradient-to-r from-green-500 to-emerald-600 text-white shadow-lg 
           hover:scale-110 hover:shadow-xl transition-transform duration-300 ease-out">
            <!-- Up Arrow Icon -->
            <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24"
                stroke="currentColor" stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round" d="M5 15l7-7 7 7" />
            </svg>
        </button>
        <transition enter-active-class="transition transform duration-700"
            enter-from-class="opacity-0 translate-y-10 scale-90" enter-to-class="opacity-100 translate-y-0 scale-100">
            <div v-if="showModal" class="fixed inset-0 bg-black/50 flex items-center justify-center z-50">
                <div class="bg-white rounded-2xl shadow-2xl max-w-4xl w-full p-8 flex gap-6 relative">


                    <div class="flex flex-col items-center">
                        <img src="/gradpic.jpg" alt="My photo"
                            class="w-60 h-60 rounded-xl shadow-lg border-4 border-green-500 object-cover transition-transform duration-500 hover:-translate-y-2 hover:shadow-2xl" />


                        <div class="mt-6 w-full text-center">
                            <h3 class="text-xl font-semibold mb-4 text-gray-800">My Stacks</h3>
                            <div class="flex flex-wrap justify-center gap-6">

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg"
                                    class="w-10 h-10" alt="Vue" />

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nuxtjs/nuxtjs-original.svg"
                                    class="w-10 h-10" alt="Nuxt" />

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/laravel/laravel-original.svg"
                                    class="w-10 h-10" alt="Laravel" />

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg"
                                    class="w-10 h-10" alt="TailwindCSS" />

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuetify/vuetify-original.svg"
                                    class="w-10 h-10" alt="Vuetify" />

                                <img src="https://flowbite.s3.amazonaws.com/logo.svg" class="w-10 h-10"
                                    alt="Flowbite" />
                            </div>
                        </div>

                        <div class="mt-8 w-full text-center">
                            <h3 class="text-xl font-semibold mb-4 text-gray-800">Programming Languages</h3>
                            <div class="flex flex-wrap justify-center gap-6">

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg"
                                    class="w-10 h-10" alt="HTML" />

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg"
                                    class="w-10 h-10" alt="CSS" />

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg"
                                    class="w-10 h-10" alt="JavaScript" />

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg"
                                    class="w-10 h-10" alt="TypeScript" />

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/php/php-original.svg"
                                    class="w-10 h-10" alt="PHP" />
                            </div>
                        </div>
                        <div class="mt-8 w-full text-center">
                            <h3 class="text-xl font-semibold mb-4 text-gray-800">Tools</h3>
                            <div class="flex flex-wrap justify-center gap-6">

                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg"
                                    class="w-10 h-10" alt="Figma" />


                                <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg"
                                    class="w-10 h-10" alt="GitHub" />


                                <img src="https://www.vectorlogo.zone/logos/getpostman/getpostman-icon.svg"
                                    class="w-10 h-10" alt="Postman" />

                                <img src="https://raw.githubusercontent.com/get-icon/geticon/master/icons/insomnia.svg"
                                    class="w-10 h-10" alt="Insomnia" />
                            </div>
                        </div>
                    </div>


                    <div class="flex-1">
                        <h2 class="text-2xl font-bold mb-4">My Skills</h2>

                        <div class="space-y-4">
                            <div v-for="skill in skills" :key="skill.name" class="p-4 rounded-xl bg-gray-100 shadow-md">
                                <h3 class="text-lg font-bold mb-2">{{ skill.name }}</h3>


                                <div class="w-full bg-gray-200 h-3 rounded-full overflow-hidden">
                                    <div class="h-3 rounded-full bg-green-500 transition-all duration-1000"
                                        :style="{ width: skill.current + '%' }"></div>
                                </div>
                                <p class="mt-2 text-sm text-gray-600">{{ skill.current }} / 100</p>
                            </div>
                        </div>
                    </div>


                    <button @click="showModal = false"
                        class="absolute top-4 right-4 text-gray-500 hover:text-gray-800 text-xl">
                        ✖
                    </button>
                </div>
            </div>
        </transition>

    </div>
    <Footer />
</template>


<style scoped>
@keyframes float {

    0%,
    100% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-4px);

    }
}

.hover\:float-animation:hover {
    animation: float 1.5s ease-in-out infinite;
}

.cursor {
    display: inline-block;
    width: 2px;
    background-color: #16a34a;
    /* Tailwind green-600 */
    margin-left: 2px;
    animation: blink 1s step-start infinite;
}

@keyframes blink {
    50% {
        opacity: 0;
    }
}
</style>