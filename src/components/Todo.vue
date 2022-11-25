<template>
  <li :class="item.done ? 'completed' : ''">
    <div class="form-check">
      <label class="form-check-label">
        <input class="checkbox" type="checkbox" :checked="item.done" @change="doTodo(item.id, $event)" />
        <i class="input-helper"></i>
        <b>{{ item.text }}</b>
        <br />
        <small>{{ item.date }}</small>
      </label>
    </div>
    <div class="ml-auto">
      <Icon
        v-show="!item.done"
        icon="akar-icons:edit"
        width="25"
        height="25"
        style="cursor: pointer"
        @click="editTodo(item.id, item.text)"
      />
      <Icon
        icon="typcn:delete-outline"
        width="25"
        height="25"
        style="cursor: pointer"
        @click="deleteTodo(item.id, item.text)"
      />
    </div>
  </li>
</template>


<script setup>
import { Icon } from "@iconify/vue";

    const props = defineProps({
        item: {
          type: Object,
          required: true,
        }
    })

    const emit = defineEmits(['edit-todo', 'delete-todo', 'do-todo'])

    function editTodo(id, oldText) {
      let newText = prompt('do edit in "' + oldText + '"');
      if(!newText) return;
      emit("edit-todo", id, newText);
    }
    function deleteTodo(id, text) {
      emit("delete-todo", id, text);
    }
    function doTodo(id, e) {
      emit('do-todo', id, e.target.checked)
    }
</script>
