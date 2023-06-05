<template>
    <aside class="todo-filters">
        <section class="toggle-group">
            <button 
                v-for="filter in filters"
                :key='filter'
                class="button "
                :class='{"button--primary": activeFilter === filter}'
                @click='setFilter(filter)'
            >{{ filter }}</button>
        </section>
    </aside>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import { Filter } from '@/types/Filter';

interface State {
    filters: Filter[]
}

export default defineComponent({
    name: 'TodoFilter',
    props: {
        activeFilter: {
            type: String as PropType<Filter>,
            required: true,
        }
    },
    data(): State {
        return {
            filters: ['All', 'Active', 'Done']
        }
    },
    methods: {
        setFilter(filter: Filter) {
            this.$emit('setFilter', filter)
        }
    },
    emits: {
        setFilter: (filter: Filter) => filter
    }
});
</script>

<style>
.todo-filters {
    display: flex;
    flex-direction: column;
    gap: 1.6rem;
}

.toggle-group {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    box-sizing: border-box;
    border: 0.1rem solid var(--light-color);
    border-radius: 1.6rem;
}

.toggle-group .button {
    font-size: 1.6rem;
}

.toggle-group .button:not(.button--primary):hover {
    color: var(--primary-color);
}
</style>
