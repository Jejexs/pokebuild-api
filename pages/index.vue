<template>
    <div class="h-24"></div>
    <div class="col-span-3">
        <SearchBar @select:pokemon="handleSelectPokemon" />
        <SearchType @update:type="handleTypeChange" />
        <div class="p-4 bg-secondary rounded-lg shadow-lg">
            <ul v-if="filteredPokemons.length > 0" class="grid grid-cols-5 gap-4 p-3 rounded-lg bg-third">
                <li v-for="pokemon in filteredPokemons" :key="pokemon.id"
                    class="relative rounded overflow-hidden shadow-md hover:shadow-xl transition-shadow duration-300 ease-in-out">
                    <img :src="pokemon.image" alt="" class="w-full h-auto">
                    <div
                        class="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center opacity-0 hover:opacity-100 transition-opacity duration-300 ease-in-out">
                        <div class="text-center text-white p-4">
                            <p class="text-lg font-bold">{{ pokemon.name }}</p>
                            <NuxtLink :to="`/${pokemon.id}`"
                                class="bg-primary text-white font-bold py-2 px-4 rounded hover:bg-blue-700 transition duration-300 inline-block text-center mt-2">
                                Plus de détails
                            </NuxtLink>
                        </div>
                    </div>
                </li>
            </ul>
            <p v-else class="text-white text-center">Problème de chargement</p>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const pokemons = ref([]);
const selectedType = ref('');

async function getPokemons() {
    try {
        const response = await fetch('https://pokebuildapi.fr/api/v1/pokemon');
        const data = await response.json();
        pokemons.value = data;
    } catch (error) {
        console.error("Erreur lors du chargement des Pokémon", error);
    }
}

const filteredPokemons = computed(() => {
    if (!selectedType.value) return pokemons.value;
    return pokemons.value.filter(p => p.types.includes(selectedType.value));
});

function handleTypeChange(type) {
    selectedType.value = type;
}

onMounted(() => {
    getPokemons();
});
</script>