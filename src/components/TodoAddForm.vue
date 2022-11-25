<template>
    <div class="add-items d-flex">
        <input type="text" class="form-control todo-list-input" placeholder="What do you need to do today?" v-model="newTodo" @keyup.enter="addTodo" />
        <button class="add btn btn-primary font-weight-bold todo-list-add-btn" @click="addTodo">
            Add
        </button>
    </div>
</template>

<script setup>
    import { ref } from "vue"
    const emit = defineEmits(['todo-text'])
    let newTodo = ref('')

    function addTodo() {
        if(!newTodo.value) return alert('type something!')
        emit('todo-text', newTodo.value)
        newTodo.value = ''
    }
</script>