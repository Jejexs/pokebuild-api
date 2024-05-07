<template>
    <div class="min-h-screen flex flex-col justify-center items-center">
        <div v-if="pokemon" class="py-10 sm:max-w-2xl sm:mx-auto">
            <div class="bg-white shadow-lg border-gray-100 border sm:rounded-3xl p-6 flex space-x-6 h-full">
                <div class="overflow-visible w-2/5">
                    <img class="rounded-3xl shadow-lg" :src="pokemon.image" alt="Image du Pokémon">
                </div>
                <div class="flex flex-col w-3/5 space-y-3 justify-between">
                    <div class="flex flex-col text-center">
                        <h2 class="text-3xl font-bold">{{ pokemon.name }}</h2>
                        <div class="flex justify-between mt-3">
                            <ul class="list-none">
                                <li v-for="type in pokemon.apiTypes" :key="type.name">
                                    <img :src="type.image" :alt="type.name" class="inline-block w-8 h-8">
                                    <span>{{ type.name }}</span>
                                </li>
                            </ul>
                        </div>
                        <div class="flex flex-grow items-center justify-center w-full p-5">
                            <ul class="text-gray-400 text-sm text-center w-full space-y-2">
                                <li>HP: {{ pokemon.stats.HP }}</li>
                                <li>Attaque: {{ pokemon.stats.attack }}</li>
                                <li>Défense: {{ pokemon.stats.defense }}</li>
                                <li>Attaque Spéciale: {{ pokemon.stats.special_attack }}</li>
                                <li>Défense Spéciale: {{ pokemon.stats.special_defense }}</li>
                                <li>Vitesse: {{ pokemon.stats.speed }}</li>
                            </ul>
                        </div>
                        <button class="mt-4 bg-blue-500 text-white py-2 px-4 rounded hover:bg-blue-600"
                            @click="addToTeam(pokemon)">
                            Ajouter à l'équipe
                        </button>
                    </div>
                </div>
            </div>
        </div>
        <div v-else class="text-primary text-center">
            <p>Chargement...</p>
        </div>
    </div>
</template>


<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const pokemonId = route.params.id;
const pokemon = ref(null);

const team = useState('team', () => []);

async function getPokemonById(pokemonId) {
    const url = `https://pokebuildapi.fr/api/v1/pokemon/${pokemonId}`;
    try {
        const response = await fetch(url);
        if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
        }
        pokemon.value = await response.json();
    } catch (error) {
        console.error('Failed to fetch Pokémon:', error);
    }
}

function addToTeam(pokemon) {
    if (team.value.length < 6 && !team.value.some(p => p.id === pokemon.id)) {
        team.value.push(pokemon);
    } else {
        alert('Votre équipe est déjà complète ou ce Pokémon est déjà ajouté.');
    }
}

onMounted(() => {
    if (pokemonId) {
        getPokemonById(pokemonId);
    }
});
</script>
