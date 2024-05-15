<template>
    <h2>Goalkeepers</h2>
    <button class="new-button">
        <i class="fa-solid fa-plus"></i>
        Create
    </button>
    <button class="delete-button">
        <i class="fa-solid fa-trash"></i>
        Delete
    </button>
</template>
<script>
export default {
    name: 'goalkeepers-component'
}
</script>
<style scoped>
h2 {
    margin: 20px;
}

.new-button {
    margin-left: 20px;
    background-color: rgb(10, 175, 10);
    color: white;
    font-weight: bold;
    border: none;
    font-size: 16px;
    padding: 15px;
    border-radius: 5px;
    box-sizing: border-box;
}

.new-button:hover {
    cursor: pointer;
    background-color: rgb(65, 213, 65);
}

.delete-button {
    margin-left: 20px;
    background-color: red;
    color: white;
    font-weight: bold;
    border: none;
    font-size: 16px;
    padding: 15px;
    border-radius: 5px;
}

.delete-button:hover {
    cursor: pointer;
    background-color: rgb(255, 118, 118);
}
</style>