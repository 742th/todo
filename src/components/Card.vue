<template>
  <li class="card">
    <input class="card__input"
      type="checkbox"
      @change="$emit('done', card.title)" />
    <p :class="['card__title', { 'completed': card.completed }]">
      <strong>{{card.id}}</strong>
      {{card.title}}
    </p>
    <del-button @deleteBtn="$emit('deleteCard', card.title)" />
  </li>
</template>

<script>
import DeleteButton from '@/components/ui/DeleteButton';
export default {
  components: {
    'del-button': DeleteButton,
  },
  props: {
    card: {
      type: Object,
      required: true,
    }
  }
}
</script>

<style scoped>
.card {
  display: flex;
  padding: 10px;
  width: 100%;
  max-width: 300px;
  border-bottom: 1px solid #000;
}

.card__input {
  margin: 0 10px 0 0;
}

.card__title {
  margin-right: 20px;
  text-align: center;
  padding-top:5px;
}
    
.completed {
  text-decoration: line-through;
}

</style>