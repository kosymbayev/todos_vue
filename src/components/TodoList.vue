<template>
    <ul class="todo-list">
        <TodoItem 
            v-for="todo in todos"
            v-bind:key='todo.id'
            :todo='todo'
            @toggle-todo='toggleTodo'
            @remove-todo='removeTodo'
        />
        <!--

            <li class="todo-item todo-item--done">
                <div class="todo-item__status">
                    <i class="bi bi-check2"></i>
                </div>
                <span class="todo-item__text">Learn the basics of Vue</span>
                <button class="todo-item__remove-button">
                <i class="bi bi-trash3"></i>
            </button>
        </li>
        <li class="todo-item">
            <div class="todo-item__status">
                <i class="bi bi-check2"></i>
            </div>
            <span class="todo-item__text">Learn the basics of Typescript</span>
            <button class="todo-item__remove-button">
                <i class="bi bi-trash3"></i>
            </button>
        </li>
        <li class="todo-item">
            <div class="todo-item__status">
                <i class="bi bi-check2"></i>
            </div>
            <span class="todo-item__text">Subscribe to the channel</span>
            <button class="todo-item__remove-button">
                <i class="bi bi-trash3"></i>
            </button>
        </li>
    -->
    </ul>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';

import TodoItem from './TodoItem.vue'

import { Todo } from '@/types/Todo';

export default defineComponent({
    name: 'TodoList',
    components: {
        TodoItem
    },
    props: {
        todos: {
            type: Array as PropType<Todo[]>
        }
    },
    methods: {
        toggleTodo(id: number) {
            this.$emit('toggleTodo', id);
        },
        removeTodo(id: number) {
            this.$emit('removeTodo', id);
        }
    },
    emits: {
        toggleTodo: (id: number) => Number.isInteger(id),
        removeTodo: (id: number) => Number.isInteger(id),
    }
});
</script>

<style>
.todo-list {
    display: grid;
    gap: 1.6rem;
    margin: 0;
    padding: 0;
    list-style: none;
}
</style>