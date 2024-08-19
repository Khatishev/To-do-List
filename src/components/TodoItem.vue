<template>
    <li class="list-note">
        <input type="text" v-model="item.note" v-if="item.edited">
        <p v-else class="note">{{ index + 1 }}. <span :class="item.done ? 'done' : ''">{{ item.note }}</span> | {{ item.date.toLocaleString() }}</p>
        <div class="btn-group">
            <input class="checkbox" v-model="item.done" type="checkbox">
            <button class="edit" @click="editNote">{{ item.edited ? '✔️' : '✏️' }}</button>
            <button class="remove-note" @click="removeNote">✖</button>
        </div>
    </li>
</template>

<script>
export default {
    name: 'TodoItem',
    props: {
        item: {
            type: Object,
            required: true
        },
        index: {
            type: Number,
            required: true
        }
    },
    methods: {
        removeNote() {
            this.$emit('removeNote', this.index);
        },
        editNote() {
            this.$emit('editNote', this.item);
        }
    }
};
</script>

<style scoped></style>