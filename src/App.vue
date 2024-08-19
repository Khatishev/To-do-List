<template>
  <div id="app">
    <TodoHeader :noteCount="todoList.length" :formattedDate="formattedDate" />
    <TodoForm v-model="inputValue" @addNote="addNote" />
    <TodoControls
      v-if="todoList.length !== 0"
      :hideCompleted="hideCompleted"
      @reverseTodoList="reverseTodoList"
      @sortedTodoList="sortedTodoList"
      @toggleHideCompleted="toggleHideCompleted"
      @clearAll="clearAll"
    />
    <h3>There are no notes, add the first one!</h3>
    <TodoList :todoList="filteredTodoList" @removeNote="removeNote" @editNote="editNote" />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';
import TodoForm from './components/TodoForm.vue';
import TodoControls from './components/TodoControls.vue';
import TodoHeader from './components/TodoHeader.vue';

export default {
  name: 'App',
  components: {
    TodoList,
    TodoForm,
    TodoControls,
    TodoHeader,
  },
  data() {
    return {
      hideCompleted: false,
      inputValue: '',
      currentDate: new Date(),
      todoList: []
    };
  },
  mounted() {
    let data = window.localStorage.getItem('todoList');
    if (data) {
      this.todoList = JSON.parse(data, (key, value) => {
        if (key === 'date') return new Date(value);
        return value;
      });
    }
    this.updateTime();
  },
  watch: {
    todoList: {
      handler: function() {
        this.saveTodoListToLocalStorage();
      },
      deep: true
    }
  },
  methods: {
    addNote() {
      if (this.inputValue.trim() !== '') {
        this.todoList.push({
          note: this.inputValue.charAt(0).toUpperCase() + this.inputValue.slice(1),
          date: new Date(),
          done: false,
          edited: false
        });
      }
      this.inputValue = '';
    },
    updateTime() {
      setInterval(() => {
        this.currentDate = new Date();
      }, 1000);
    },
    removeNote(index) {
      this.todoList.splice(index, 1);
    },
    reverseTodoList() {
      this.todoList.reverse();
    },
    clearAll() {
      this.todoList = [];
    },
    sortedTodoList(sortBy) {
      if (sortBy === 'note') {
        this.todoList.sort((a, b) => (a.note > b.note) ? 1 : -1);
      } else if (sortBy === 'date') {
        this.todoList.sort((a, b) => new Date(a.date) - new Date(b.date));
      }
    },
    editNote(item) {
      item.edited = !item.edited;
    },
    saveTodoListToLocalStorage() {
      window.localStorage.setItem('todoList', JSON.stringify(this.todoList));
    },
    toggleHideCompleted() {
      this.hideCompleted = !this.hideCompleted;
    }
  },
  computed: {
    filteredTodoList() {
      let result = this.inputValue;
      return this.todoList.filter((elem) => {
        if (result === '') { return true; }
        else return elem.note.toUpperCase().indexOf(result.toUpperCase()) > -1;
      }).filter((t) => !this.hideCompleted || !t.done);
    },
    formattedDate() {
      return this.currentDate.toLocaleTimeString('ru-RU', { weekday: 'long', day: 'numeric', month: 'numeric', year: 'numeric', hour: 'numeric', minute: 'numeric' });
    }
  }
};
</script>

<style></style>