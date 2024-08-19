<template>
    <div class="list">
      <ul>
        <TodoItem
          v-for="(item, index) in todoList"
          :key="index"
          :item="item"
          :index="index"
          @removeNote="removeNote"
          @editNote="editNote"
        />
      </ul>
    </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
    name: 'TodoList',
    components: {
        TodoItem
    },
    props: {
        todoList: {
            type: Array,
            required: true
        }
    },
    methods: {
        removeNote(index) {
            this.$emit('removeNote', index);
        },
        editNote(item) {
            this.$emit('editNote', item);
        }
    }
};
</script>
  
<style scoped></style>