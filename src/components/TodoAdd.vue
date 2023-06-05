<template>
    <section class="add-todo">

        <form 
            v-if="isFormVisible"
            class="add-todo__form"
            @submit.prevent='addTodo'
        >
            <button 
                class="close-button" 
                type="button"
                @click='hideForm'
            >
                <i class="bi bi-x"></i>
            </button>
            <div class="text-input text-input--focus">
                <input 
                    v-model="todoText"
                    class="input" 
                />
            </div>
            <button class="button button--filled">Add task</button>
        </form>
        <button 
            v-else
            class="add-todo__show-form-button"
            @click='showForm'
        >
            <i class="bi bi-plus-lg"></i>
        </button>
    </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import { Todo } from '@/types/Todo';

interface State {
    isFormVisible: boolean,
    todoText: string,
}

export default defineComponent({
    name: 'TodoAdd',
    data(): State {
        return {
            isFormVisible: false,
            todoText: '',
        }
    },
    methods: {
        showForm() {
            this.isFormVisible = true;
        },
        hideForm() {
            this.isFormVisible = false;
        },
        addTodo() {
            this.$emit('addTodo', {
                id: Date.now(),
                text: this.todoText,
                completed: false,
            });
            this.todoText = '';
            //this.hideForm();
        }
    },
    emits: {
        addTodo: (todo: Todo) => todo
    }
});
</script>

<style>
.add-todo {
    display: grid;
    gap: 1.6rem;
}

.add-todo__show-form-button {
    grid-template-columns: 1fr;
    justify-items: center;
    padding: 1.2rem 1.4rem;
    color: var(--primary-color);
    font-size: 1.9rem;
    border: 0.1rem solid var(--light-color);
    border-radius: 1.6rem;
    transition: box-shadow 0.2s;
}

.add-todo__show-form-button:hover {
    box-shadow: 0px 1px 20px rgb(240 240 240 / 80%);
}

.add-todo__form {
    display: grid;
    gap: 1.6rem;
    padding: 1.4rem 1.6rem 2rem;
    border: 0.1rem solid var(--light-color);
    border-radius: 1.6rem;
    box-shadow: 0px 1px 20px rgb(240 240 240 / 80%);
}

.add-todo__form .close-button {
    justify-self: end;
    font-size: 2rem;
}

.add-todo__form .close-button:hover {
    color: var(--primary-color);
}
</style>