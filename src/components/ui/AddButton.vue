<template>
  <button class="add__button" @click="$emit('addBtn')">+</button>
</template>

<script>
export default {
        
}
</script>

<style scoped>
.add__button {
  border-radius: 50%;
  font-size: 20px;
  background-color: rgb(12, 112, 151);
}
.add__button:hover {
  cursor: pointer;
  opacity: 0.7;
}
</style>