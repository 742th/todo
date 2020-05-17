<template>
  <div id="app">
    <h1 class="title">ToDo-test</h1>
    <form class="form" @submit.prevent="onSubmit">
      <input class="form__input" placeholder="Введите название списка дел" v-model="text"/>
      <AddButton @addButton="onSubmit"/>
    </form>
    <hr>
    <section class="container">
      <Todos v-for="(el, i) of mainArray" 
      :el="el"
      :number="i" 
      :key="i"
      @new-item="addItem"
      @deleteBtn="deleteItem" 
      @delete-card="deleteCard"
      @done="toggleComplete"
      />
    </section>
  </div>
</template>

<script>
import Todos from '@/components/Todos';
import AddButton from './components/ui/AddButton';

export default {
  name: 'App',
  components: {
    Todos,
    AddButton,
  },
  data() {
    return {
      text: '',
      mainArray: [{ 
        title: 'nice try', 
        todos:[
          {id:1, title: 'Устроиться', completed: false},
          {id:2, title: 'в', completed: false},
          {id:3, title: 'ProContext', completed: false},
          {id:4, title: '(0_0)', completed: false},]
        }],
    }
  },
  methods: {
    onSubmit() {
      if (!this.text.length) {
        return;
      }
      const newItem = { title: this.text, todos: [] }
      this.mainArray.push(newItem);
      this.text = '';
    },
    addItem (el) {
      const item = this.mainArray.find((item, index)=> index === el._id);
      item.todos.push(el);
    },
    deleteItem (value) {
      this.mainArray = this.mainArray.filter((el, index) => index !== value);
    },
    deleteCard (item) {
      const { id, value } = item;
      this.mainArray[value].todos = this.mainArray[value].todos.filter((el) => el.title !== id);
    },
    toggleComplete(item) {
      const { id, value } = item;
      const el = this.mainArray[value].todos.find((el) => el.title === id);
      return el.completed = !el.completed;
    }
  }
}
</script>

<style>
#app {
  font-family: Inter, Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  background-color: #037a49;
  color: #fff;
}
*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.container {
  max-width: 1440px;
  margin: 30px auto 0;
  display: flex;
  flex-wrap: wrap;
}

#app {
  padding: 20px 10px 0;
}

.form {
  margin-bottom: 10px;
}

.form__input {
  width: 200px;
  margin-right: 10px;
}

@media screen and (max-width: 768px) {
  .container {
    flex-direction: column;
    align-items: center;
  }
}
</style>
