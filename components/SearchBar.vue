<template>
    <div class="search-bar">
        <input type="text" v-model="searchTerm" placeholder="Rechercher un Pokémon par nom..."
            class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-blue-500" />
        <div v-if="filteredPokemons.length > 0" class="mt-2">
            <ul>
                <li v-for="pokemon in filteredPokemons" :key="pokemon.id" class="py-2">
                    <button @click="selectPokemon(pokemon)" class="text-blue-500 hover:text-blue-700">{{ pokemon.name
                        }}</button>
                </li>
            </ul>
        </div>
        <p v-else class="mt-2 text-gray-500">Aucun Pokémon trouvé.</p>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const searchTerm = ref('');
const pokemons = ref([]);

const filteredPokemons = computed(() => {
    if (!searchTerm.value.trim()) return pokemons.value;
    return pokemons.value.filter(pokemon =>
        pokemon.name.toLowerCase().includes(searchTerm.value.toLowerCase())
    );
});

function selectPokemon(pokemon) {
    emit('select:pokemon', pokemon);
}

const emit = defineEmits(['select:pokemon']);
</script>

<style scoped>
.search-bar {
    max-width: 400px;
    margin: 0 auto;
}
</style>