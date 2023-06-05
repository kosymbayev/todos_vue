<template>
    <TheHeader />

    <TodoFilter 
        :active-filter="activeFilter"
        @set-filter='setFilter'
    />

    <main class="app-main">
        <TodoList 
            :todos='filteredTodos'
            @toggle-todo='toggleTodo'
            @remove-todo='removeTodo'
        />
        <TodoAdd 
            @add-todo='addTodo'
        />
    </main>

    <TheFooter :stats='stats'/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import TheHeader from './components/TheHeader.vue'
import TodoFilter from './components/TodoFilter.vue'
import TodoList from './components/TodoList.vue'
import TodoAdd from './components/TodoAdd.vue'
import TheFooter, { Stats } from './components/TheFooter.vue'

import { Todo } from '@/types/Todo';
import { Filter } from './types/Filter';

interface State {
    todos: Todo[]
    activeFilter: Filter
}

export default defineComponent({
    name: 'App',
    components: {
        TheHeader,
        TodoFilter,
        TodoList,
        TodoAdd,
        TheFooter,
    },
    data(): State {
        return {
            todos: [
                {id: 0, text: `Learn the basics of Vue`, completed: true},
                {id: 1, text: `Learn the basics of Typescript`, completed: false},
                {id: 2, text: `Make Todo App`, completed: false}
            ],
            activeFilter: 'All',
        }
    },
    computed: {
        activeTodos(): Todo[] {
            return this.todos.filter(todo => !todo.completed)
        },
        doneTodos(): Todo[] {
            return this.todos.filter(todo => todo.completed)
        },
        filteredTodos(): Todo[] {
            switch (this.activeFilter) {
                case 'Active':
                    return this.activeTodos
                case 'Done':
                    return this.doneTodos
                case 'All':
                default:
                    return this.todos
            }
        },
        stats(): Stats {
            return {
                active: this.activeTodos.length,
                done: this.doneTodos.length
            }

        }
    },
    methods: {
        toggleTodo(id: number) {
            const targetTodo = this.todos.find((todo: Todo) => todo.id === id)
            
            if (targetTodo) {
                targetTodo.completed = !targetTodo.completed
            }
        },
        removeTodo(id: number) {
            this.todos = this.todos.filter((todo: Todo) => todo.id !== id)
        },
        addTodo(todo: Todo) {
            this.todos.push(todo)
        },
        setFilter(filter: Filter) {
            this.activeFilter = filter
        }
    }
});
</script>

<style>
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.4/font/bootstrap-icons.css");
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap');

:root {
    --primary-color: #092567;
    --secondary-color: #e3e3e3;
    --light-color: #f0f0f0;
    --reverse-color: #ffffff;
    --default-color: #000000;
}

html {
    font-size: 62.5%;
}

body {
    display: flex;
    justify-content: center;
    margin: 0;
    padding: 6.4rem 1.2rem;
    font-family: 'Roboto', sans-serif;
    font-size: 1.6rem;
    color: var(--default-color)
}

button {
    padding: 0;
    font: inherit;
    background-color: transparent;
    border: none;
    cursor: pointer;
}

.button {
    font-size: 1.6rem;
    padding: 0.6rem 1rem;
    border-radius: 1.6rem;
}

.button--primary {
    color: var(--primary-color);
    border: 2px solid var(--primary-color);
}

.button--filled {
    padding: 0.8rem 1rem;
    color: var(--reverse-color);
    background-color: var(--primary-color);
}

.button--primary:hover {
    opacity: 0.8;
}

#app {
    display: flex;
    flex-direction: column;
    gap: 3.2rem;
    width: 34rem;
}

.text-input {
    display: flex;
    align-items: center;
    padding: 0.8rem 1.6rem;
    box-sizing: border-box;
    font: inherit;
    font-size: 1.6rem;
    border: 0.1rem solid var(--light-color);
    border-radius: 1.6rem;
}

.text-input--focus {
    border: 0.2rem solid var(--primary-color);
}

.text-input .input {
    flex-grow: 1;
    padding: 0;
    border: none;
}

.text-input .input:focus {
    outline: none;
}

.app-main {
    display: grid;
    gap: 1.6rem;
}
</style>
