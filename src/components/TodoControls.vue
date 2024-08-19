<template>
    <div class="main">
      <button class="methods" @click="$emit('reverseTodoList')">Reverse</button>
      <button class="methods" @click="$emit('sortedTodoList', 'note')">Sort</button>
      <button class="methods" @click="$emit('sortedTodoList', 'date')">Sort by date</button>
      <button class="methods" @click="$emit('toggleHideCompleted')">{{ hideCompleted ? 'Show all' : 'Hide completed' }}</button>
      <button class="methods" @click="$emit('clearAll')">Clear all</button>
    </div>
</template>

<script>
export default {
    name: 'TodoControls',
    props: {
        hideCompleted: {
            type: Boolean,
            required: true
        }
    },
    emits: ['reverseTodoList', 'sortedTodoList', 'toggleHideCompleted', 'clearAll']
};
</script>

<style scoped></style>