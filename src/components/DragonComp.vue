<script setup>
import { ref } from "vue";
const props = defineProps({
    name: String,
    image: String,
    skills: String,
    id: Number
})

const emit = defineEmits(["renameDragon", "deleteDragon"])

const newDragonName = ref("")

function handleSubmit() {
    emit("renameDragon", props.id, newDragonName.value)
}

function handleDelete() {
    emit("deleteDragon", props.id)
}
</script>

<template>
<article>
    <div class="grid">
    <i class="fa-regular fa-trash-can" @click="handleDelete"></i>
    <h2>{{name}}</h2>
    <img :src="image" :alt="name">
    <p>{{ skills }}</p>
    </div>
    <form @submit.prevent="handleSubmit">
        <div>
        <label for="betterName">Rename to:</label>
        <input id="betterName" type="text" placeholder="Better name..."
        v-model="newDragonName">
        </div>
        <input type="submit" value="Update name" >
    </form>
</article>
</template>

<style scoped>
article {
    border: 2px solid red;
    border-radius: 5px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    img {
        max-width: 400px;
    }

    .grid {
    display: flex;
    align-items: center;
    flex-direction: column;
    }

    form {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    [type="text"] {
        padding: 0.5rem;
        border-radius: 5px;
        border: 2px solid black;
    }

    [type="submit"] {
        background-color: red;
        color: white;
        border: none;
        padding: 1rem;
        border-radius: 10px;
        cursor: pointer;
    }

    i {
        color: red;
        font-size: 1.5rem;
        align-self: flex-end;
        cursor: pointer;
    }
}
</style>