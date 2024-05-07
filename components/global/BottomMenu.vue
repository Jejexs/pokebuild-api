<template>
    <div
        class="fixed z-50 w-full h-20 max-w-lg -translate-x-1/2 bg-white border border-gray-200 rounded-full bottom-4 left-1/2 dark:bg-gray-700 dark:border-gray-600">
        <div class="grid h-full max-w-lg grid-cols-2 mx-auto">
            <NuxtLink to="/" data-tooltip-target="tooltip-wallet" type="button"
                class="inline-flex flex-col items-center rounded-s-full justify-center px-5 hover:bg-gray-50 dark:hover:bg-gray-800 group">
                <img src="/pokedex.png" alt="Pokedex" class=" h-16" />
                <span class="sr-only">Catalogue</span>
            </NuxtLink>
            <div id="tooltip-wallet" role="tooltip"
                class="absolute z-10 invisible inline-block px-3 py-2 text-sm font-medium text-white transition-opacity duration-300 bg-gray-900 rounded-lg shadow-sm opacity-0 tooltip dark:bg-gray-700">
                <div class="tooltip-arrow" data-popper-arrow></div>
            </div>
            <NuxtLink to="/teams" data-tooltip-target="tooltip-profile" type="button"
                class="inline-flex flex-col items-center justify-center px-5 rounded-e-full hover:bg-gray-50 dark:hover:bg-gray-800 group">
                <img src="/teams.png" alt="Teams" class=" h-16" />
                <span class="sr-only">Team</span>
            </NuxtLink>
            <div id="tooltip-profile" role="tooltip"
                class="absolute z-10 invisible inline-block px-3 py-2 text-sm font-medium text-white transition-opacity duration-300 bg-gray-900 rounded-lg shadow-sm opacity-0 tooltip dark:bg-gray-700">
                <div class="tooltip-arrow" data-popper-arrow></div>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>


<script setup>

</script>