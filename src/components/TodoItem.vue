<template>
    <li 
        class="todo-item" 
        :class="{'todo-item--done': todo.completed}"
        @click='toggleTodo()'
        >
        <div class="todo-item__status">
            <i class="bi bi-check2"></i>
        </div>
        <span class="todo-item__text">{{ todo.text }}</span>
        <button 
            class="todo-item__remove-button"
            @click.stop='removeTodo()'
        >
            <i class="bi bi-trash3"></i>
        </button>
    </li>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import { Todo } from '@/types/Todo';

export default defineComponent({
    name: 'TodoItem',
    props: {
        todo: {
            type: Object as PropType<Todo>,
            required: true,
        }
    },
    methods: {
        toggleTodo() {
            this.$emit('toggleTodo', this.todo.id)
        },
        removeTodo() {
            this.$emit('removeTodo', this.todo.id)
        }
    },
    emits: {
        toggleTodo: (id: number) => Number.isInteger(id),
        removeTodo: (id: number) => Number.isInteger(id),
    }
});
</script>

<style>
.todo-item {
    display: grid;
    grid-template-columns: 2.4rem 1fr 1.6rem;
    align-items: center;
    gap: 1.6rem;
    padding: 1.6rem 2rem;
    border: 0.1rem solid var(--light-color);
    border-radius: 1.6rem;
    transition: box-shadow 0.2s;
    cursor: pointer;
}

.todo-item:hover {
    box-shadow: 0px 1px 20px rgb(240 240 240 / 80%);
}

.todo-item__text {
    font-weight: 400;
    word-break: break-word;
}

.todo-item--high .todo-item__text {
    font-weight: 500;
}

.todo-item--low .todo-item__text {
    font-weight: 300;
}

.todo-item--done .todo-item__text {
    text-decoration: line-through;
}

.todo-item__status {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 2.4rem;
    height: 2.4rem;
    font-size: 2.4rem;
    opacity: 0;
    transition: opacity 0.2s;
}

.todo-item__status .bi-check2 {
    position: relative;
    top: 0.1rem;
    color: var(--primary-color)
}

.todo-item--done .todo-item__status {
    opacity: 1;
}

.todo-item:hover .todo-item__status {
    opacity: 1;
}

.todo-item--done .todo-item__status .bi-check2 {
    display: block;
}

.todo-item__remove-button {
    opacity: 0;
    color: var(--secondary-color);
    transition: opacity 0.2s;
}

.todo-item:hover .todo-item__remove-button {
    opacity: 1;
}

.todo-item__remove-button:hover {
    color: var(--primary-color);
}
</style>