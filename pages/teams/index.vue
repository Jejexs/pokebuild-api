<template>
    <div class="min-h-screen flex flex-col items-center justify-center">
        <h1 class="text-4xl font-bold mb-8">Mon Équipe Pokémon</h1>
        <div class="grid grid-cols-3 gap-4 w-full max-w-4xl p-4">
            <div v-for="pokemon in team" :key="pokemon.id"
                class="team-slot bg-white shadow-lg rounded-lg p-4 flex flex-col items-center justify-center">
                <img :src="pokemon.image" alt="" class="w-32 h-32">
                <p class="mt-2 font-semibold">{{ pokemon.name }}</p>
            </div>
            <div v-for="empty in 6 - team.length" :key="`empty-${empty}`"
                class="team-slot bg-gray-200 flex items-center justify-center">
                <span class="text-gray-500">Vide</span>
            </div>
        </div>
    </div>
</template>

<script setup>

const team = useState('team', () => {
    return JSON.parse(window.localStorage.getItem('team') || '[]');
});

watch(team, (newTeam) => {
    window.localStorage.setItem('team', JSON.stringify(newTeam));
}, { deep: true });

</script>

<style scoped>
.team-slot {
    height: 200px;
}
</style>
