<template>
    <div class="type-selector flex flex-wrap justify-center" v-if="types.length > 0">
        <button v-for="type in types" :key="type.name" @click="selectType(type.name)"
            :class="{ 'selected': selectedType === type.name }"
            class="relative flex items-center justify-center w-24 h-24 rounded-lg overflow-hidden shadow-md m-2 bg-white border border-gray-300 hover:border-blue-500">
            <img :src="type.image" alt="Type Image"
                class="absolute inset-0 w-full h-full object-cover transition-opacity duration-300 ease-in-out opacity-100 hover:opacity-75" />
            <span
                class="absolute bottom-0 left-0 right-0 p-2 bg-black bg-opacity-50 text-white text-center font-bold uppercase">
                {{ type.name }}
            </span>
        </button>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const types = ref([]);
const selectedType = ref('');

async function fetchTypes() {
    try {
        const response = await fetch('https://pokebuildapi.fr/api/v1/types');
        if (!response.ok) {
            throw new Error('Failed to fetch types');
        }
        const data = await response.json();
        types.value = data;
    } catch (error) {
        console.error('Error fetching types:', error);
    }
}

onMounted(() => {
    fetchTypes();
});

function selectType(type) {
    selectedType.value = type;
    emit('update:type', type);
}

const emit = defineEmits(['update:type']);
</script>

<style scoped>
.type-selector .selected {
    border-color: #007bff;
}
</style>