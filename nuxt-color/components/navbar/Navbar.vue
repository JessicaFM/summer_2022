<template>
    <nav class="flex items-center justify-between flex-wrap bg-black p-6">
        <div class="container mx-auto flex">
            <div class="flex items-center flex-shrink-0 text-white mr-6">
                <span class="font-semibold text-xl tracking-tight">
                    <NuxtLink to="/">
                        Nuxt Colors
                    </NuxtLink>
                </span>
            </div>
            <div class="w-full block flex-grow lg:flex lg:items-center lg:w-auto">
                <div class="text-sm lg:flex-grow">
                    <NuxtLink to="/custom"
                    class="block mt-4 lg:inline-block lg:mt-0 text-teal-200 hover:text-white mr-4">
                        Generate templates
                    </NuxtLink>
                </div>
            </div>
        </div>
    </nav>   
</template>

<script>
    export default {
        name: 'NavBar'
    }
</script>
