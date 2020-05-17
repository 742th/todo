<template>
  <ul class="todos" >
    <div>
      <DeleteButton @deleteBtn="$emit('deleteBtn', value)"/>
      <h2 class="todos__title">{{element.title}}</h2>
      <form class="form" @submit.prevent="addTodo">
        <input class="form__input" placeholder="Введите задачу" v-model="text" />
        <AddButton />
      </form>
      <select v-model="choose" class="choose">
        <option value="all">all</option>
        <option value="completed">Completed</option>
        <option value="not completed">Not Completed</option>
        <option value="alphabet">alphabet</option>    
      </select>
    </div>
    <Card v-for="card in changeFilter" 
    :card="card" 
    :key="card.id"
    @deleteCard="deleteCard"
    @done="done"
    />
  </ul>
</template>

<script>
import Card from './Card';
import AddButton from './ui/AddButton';
import DeleteButton from './ui/DeleteButton';
export default {
  components: {
    Card,
    DeleteButton,
    AddButton,
  },
  props: {
    'el': {
      type: Object,
      required: true,
    },
    'number': {
      type: Number,
      required: true,
    }
  },
  data() {
    return {
      value: this.number,
      text: '',
      element: this.el,
      choose: 'all'
    }
  },
  computed: {
    // eslint-disable-next-line vue/return-in-computed-property
    changeFilter () {
      switch (this.choose) {
        case 'all': 
          return this.element.todos;
          // eslint-disable-next-line no-unreachable
          break;
        case 'completed':
          return this.element.todos.filter(el => el.completed);
          // eslint-disable-next-line no-unreachable
          break;
        case 'not completed':
          return this.element.todos.filter(el => !el.completed);
          // eslint-disable-next-line no-unreachable
          break;
        case 'alphabet':
          // eslint-disable-next-line vue/no-side-effects-in-computed-properties
          return this.element.todos.sort((a, b) => a.title.localeCompare(b.title, 'ru-RU'));
          // eslint-disable-next-line no-unreachable
          break;
      }
    },

  },
  methods: {
    addTodo () {
      if (!this.text.length) {
        return;
      }
      const newItem = {
        _id: this.value,
        title: this.text,
        completed: false
      };
      this.$emit('new-item', newItem);
      this.text = '';
    },
    deleteCard (id) {
      const item = {
        id,
        value: this.value,
      }
      this.$emit('delete-card', item);
    },
    done (id) {
      const item = {
        id,
        value: this.value,
      };
      this.$emit('done', item);
    }
  }
}
</script>

<style scoped>
  .todos {
    margin: 0 20px 30px 0;
    border: 2px solid #000;
    padding: 5px;
    border-radius: 10px;
    box-shadow: 0 0 10px #000;
  }

  .todos__title {
    border-bottom: 2px solid #000;
    padding: 5px;
    max-width: 200px;
  }

  .form__input {
    margin-right: 7px;
  }
</style>