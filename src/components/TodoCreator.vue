<script setup>
import { reactive, ref } from 'vue';
import TodoButton from './TodoButton.vue'
const todo = ref("")
const emit = defineEmits(["create-todo"]);
const todoState = reactive({
    todo: "",
    invalid: null,
    errmsg: ""
})

const createTodo = () => {
    todo.invalid = null;
    if (todoState.todo !== "") {
        emit("create-todo", todoState.todo);
        todoState.todo = "";
        return
    }
    todoState.invalid = true;
    todoState.errmsg = "Todo value can not be empty"
}
</script>
<template>
    <div class="input-wrap" :class="{ 'input-err': todoState.invalid }">
        <input type="text" v-model="todoState.todo">
        <!-- <input type="text" v-model="todo"> -->
        <TodoButton @click="createTodo()" />
    </div>
    <!-- <p>{{ todoState }}</p> -->
    <p>{{ todo }}</p>
    <p class="err-msg" v-if="todoState.invalid">{{ todoState.errmsg }}</p>
</template>
<style lang="scss" scoped>
.input-wrap {
    display: flex;
    transition: 250ms ease;
    border: 2px solid #41b080;

    &.input-err {
        border-color: red;
    }

    &:focus-within {
        box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
            0 -2px 4px -2px rgb(0 0 0 / 0.1);
    }

    input {
        width: 100%;
        padding: 8px 6px;
        border: none;

        &:focus {
            outline: none;
        }
    }

    
}

.err-msg {
    margin-top: 6px;
    font-size: 12px;
    text-align: center;
    color: red;
}</style>