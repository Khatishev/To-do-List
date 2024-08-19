<template>
    <div class="form">
      <input class="inp-add-note" type="text" placeholder="Next note?" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" @keypress.enter="$emit('addNote')">
      <button class="btn-add-note" @click="$emit('addNote')">+</button>
    </div>
</template>

<script>
export default {
    name: 'TodoForm',
    props: {
        modelValue: {
            type: String,
            required: true
        }
    },
    emits: ['update:modelValue', 'addNote']
};
</script>

<style scoped></style>