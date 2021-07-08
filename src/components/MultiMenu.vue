<template>
    <div class="flex flex-col md:items-center w-full h-screen md:h-auto">
        <nav class="w-full md:w-1/2 md:bg-gray-300 fixed md:relative flex flex-col md:flex-row md:justify-evenly items-end md:items-start border-b-4 border-black mt-2 shadow rounded-md">
            
            <span class="w-full mr-2 md:mr-0 my-1 md:my-0 flex flex-col items-end md:items-start">
                <button
                    class="w-full h-10 transiton-all duration-150 bg-gray-300 rounded md:rounded-none hover:bg-gray-200 flex items-center justify-center"
                    @click="toggleMenu('profile')"
                > <i class="far fa-user"></i><h2 class="ml-2">profile</h2>
                </button>
                <transition name="dropdown">
                    <div v-if="menu.profile.dropdown" class="md:absolute mt-1 md:mt-10 mb-1 md:mb-0 md:flex">
                        <span class="flex flex-col w-48">
                            <span :class="{ 'bg-gray-100': menu.profile.posts_drop}"
                                class="w-full z-20 flex items-center justify-between py-2 px-6 border-b-2 border-black shadow transition duration-150 mt-1 transform -translate-x-1 md:translate-x-0 hover:translate-x-1 rounded bg-gray-300 hover:bg-gray-100 text-left">
                                <button>
                                    posts
                                </button>
                                <button
                                    @click="menu.profile.posts_drop = !menu.profile.posts_drop"
                                >
                                    <svg
                                        aria-hidden="true"
                                        width="12"
                                        focusable="false"
                                        :class="{
                                            'arrow_open': menu.profile.posts_drop,
                                        }"
                                        data-prefix="fas"
                                        data-icon="angle-right"
                                        class="svg-inline--fa transition-all duration-400 ease-in-out fa-angle-right fa-w-8"
                                        role="img"
                                        xmlns="http://www.w3.org/2000/svg"
                                        viewBox="0 0 256 512"
                                    >
                                        <path
                                            fill="currentColor"
                                            d="M224.3 273l-136 136c-9.4 9.4-24.6 9.4-33.9 0l-22.6-22.6c-9.4-9.4-9.4-24.6 0-33.9l96.4-96.4-96.4-96.4c-9.4-9.4-9.4-24.6 0-33.9L54.3 103c9.4-9.4 24.6-9.4 33.9 0l136 136c9.5 9.4 9.5 24.6.1 34z"
                                        >
                                        </path>
                                    </svg>
                                </button>
                            </span>
                            <transition name="slideopen">
                                <div v-if="menu.profile.posts_drop" class="flex flex-col items-end my-1 transform">
                                    <button class="w-full h-10 px-2 border border-gray-700 bg-gray-100 hover:bg-gray-100 transition-all transform hover:scale-105 -translate-x-3 md:translate-x-1 hover:translate-x-3 duration-150 text-left shadow-sm rounded-md mb-1">new post</button>
                                    <button class="w-full h-10 px-2 border border-gray-700 bg-gray-100 hover:bg-gray-100 transition-all transform hover:scale-105 -translate-x-3 md:translate-x-1 hover:translate-x-3 duration-150 text-left shadow-sm rounded-md">control</button>
                                </div>
                            </transition>
                            <button
                                class="w-full z-30 py-2 px-6 border-b-2 border-black shadow transition duration-150 mt-1 transform -translate-x-1 md:translate-x-0 hover:translate-x-1 rounded bg-gray-300 hover:bg-gray-100 text-left"
                            >stats</button>
                            <button
                                class="w-full z-30 py-2 px-6 border-b-2 border-black shadow transition duration-150 mt-1 transform -translate-x-1 md:translate-x-0 hover:translate-x-1 rounded bg-gray-300 hover:bg-gray-100 text-left"
                            >contacts</button>
                        </span>
                    </div>
                </transition>
            </span>
            <span class="w-full mr-2 md:mr-0 flex flex-col items-end my-1 md:my-0">
                <button
                    class="w-full h-10 transiton-all bg-gray-300 duration-150 rounded md:rounded-none hover:bg-gray-200" 
                    @click="toggleMenu('central')"
                >central
                </button>
                <transition name="dropdown-central">
                    <div v-if="menu.central.dropdown" class="flex flex-col md:absolute mt-1 md:mt-10 mb-1 md:mb-0">
                        <span>
                            <button class="w-full mr-2 py-2 px-6 border-b-2 border-black shadow transition duration-150 mt-1 transform hover:translate-x-1 rounded bg-gray-300 hover:bg-gray-100 text-left">stats</button>
                            <button class="w-full mr-2 py-2 px-6 border-b-2 border-black shadow transition duration-150 mt-1 transform hover:translate-x-1 rounded bg-gray-300 hover:bg-gray-100 text-left">contacts</button>
                        </span>
                    </div>
                </transition>
            </span>
            <span class="w-full mr-2 md:mr-0 my-1 md:my-0">
                <button class="w-full h-10 transiton-all duration-150 bg-gray-300 rounded md:rounded-none hover:bg-gray-200">login</button>
            </span>
        
        </nav>
    </div>
</template>
<script>
    export default ({
        name: 'MultiMenu.vue',
        data() {
            return {
                menu: {
                    profile: {
                        dropdown: false,
                        posts_drop: false
                    },
                    central: {
                        dropdown: false
                    }
                },

            }
        },
        methods: {
            toggleMenu(menu)
            {
                this.menu[menu].dropdown = !this.menu[menu].dropdown;
                if (menu === 'profile' && this.menu[menu].posts_drop === true) this.menu[menu].posts_drop = false;
                Object.keys(this.menu).forEach(key => {
                    if (this.menu[key].dropdown === true && key !== menu) {
                        this.menu[key].dropdown = false;
                    }
                })
            }
        }
    });
</script>
<style scoped>
    .dropdown-enter-from {
        margin-top: -142px;
        opacity: 0;
    }
    .dropdown-enter-to {
        margin-top: 0px;
        opacity: 1;
    }
    .dropdown-enter-active {
        transition: margin-top 350ms, opacity 200ms ease-in 100ms;
    }
    .dropdown-leave-active {
        transition: margin-top 350ms, opacity 100ms;
    }
    .dropdown-leave-to {
        margin-top: -142px;
        opacity: 0;
    }
    .dropdown-central-enter-from {
        margin-top: -96px;
        opacity: 0;
    }
    .dropdown-central-enter-to {
        margin-top: 0px;
        opacity: 1;
    }
    .dropdown-central-enter-active {
        transition: margin-top 350ms, opacity 200ms ease-in 100ms;
    }
    .dropdown-central-leave-active {
        transition: margin-top 350ms, opacity 100ms;
    }
    .dropdown-central-leave-to {
        z-index: -1;
        margin-top: -96px;
        opacity: 0;
    }

    .slideopen-enter-active {
        transition: opacity 150ms ease-in 100ms, margin-top 350ms;
    }
    .slideopen-leave-active {
        transition: opacity 150ms ease-in, margin-top 350ms;
    }
    .slideopen-enter-from {
        margin-top: -76px;
        opacity: 0;
    }
    .slideopen-enter-to {
        margin-top: 0px;
        opacity: 1;
    }
    .slideopen-leave-from {
        margin-top: 0px;
        opacity: 1;
    }
    .slideopen-leave-to {
        margin-top: -76px;
        opacity: 0;

    }
    .arrow_open {
        transform: rotate(540deg);
    }
    @media only screen and (min-width: 768px) {
        .dropdown-enter-from {
            margin-top: -2.5rem;
            z-index: -1;
            opacity: 0;
        }
        .dropdown-enter-to {
            margin-top: 2.5rem;
            opacity: 1;
        }
        .dropdown-enter-active {
            transition: opacity 200ms ease-in 100ms , margin-top 350ms;
        }
        .dropdown-leave-active {
            transition: opacity 100ms ease-in , margin-top 350ms;
        }
        .dropdown-leave-to {
            margin-top: -2.5rem;
            opacity: 0;
        }
        .dropdown-central-enter-from {
            margin-top: -2.5rem;
            z-index: -1;
            opacity: 0;
        }
        .dropdown-central-enter-to {
            margin-top: 2.5rem;
            z-index: -1;
            opacity: 1;
        }
        .dropdown-central-enter-active {
            transition: margin-top 350ms, opacity 200ms ease-in 100ms;
        }
        .dropdown-central-leave-active {
            transition: margin-top 350ms, opacity 100ms;
        }
        .dropdown-central-leave-to {
            z-index: -1;
            margin-top: -2.5rem;
            opacity: 0;
        }
        .slideopen-enter-active {
            transition: opacity 150ms ease-out 100ms, margin-top 350ms, margin-bottom 350ms;
        }
        .slideopen-leave-active {
            transition: opacity 150ms ease-in, margin-top 350ms, margin-bottom 350ms;
        }
        .slideopen-enter-from {
            margin-top: -5rem;
            opacity: 0;
            margin-bottom: 0rem;
        }
        .slideopen-enter-to {
            margin-top: 0.3rem;
            margin-bottom: 0.25rem;
            opacity: 1;
        }
        .slideopen-leave-from {
            margin-top: 0.3rem;
            margin-bottom: 0.25rem;
            opacity: 1;
        }
        .slideopen-leave-to {
            margin-top: -5rem;
            opacity: 0;
            margin-bottom: 0rem;
        }
        .arrow_open {
            transform: rotate(540deg);
        }
    }

</style>
