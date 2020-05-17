<template>
  <button class="delete__button" @click="$emit('deleteBtn')">-</button>
</template>

<script>
export default {
        
}
</script>

<style scoped>
.delete__button {
  border-radius: 50%;
  font-size: 20px;
  background-color: rgb(148, 35, 35);
  border: none;
  box-shadow: 0 0 5px #000;
}

.delete__button:hover {
  cursor: pointer;
  opacity: 0.7;
}
</style>