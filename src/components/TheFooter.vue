<template>
    <footer class="footer">{{ stats.active }} more to do, {{ stats.done }} done</footer>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';

export interface Stats {
    active: number,
    done: number,
}
export default defineComponent({
    name: 'TheFooter',
    props: {
        stats: {
            type: Object as PropType<Stats>,
            required: true
        }
    }
});
</script>

<style>
.footer {
    font-size: 1.4rem;
    text-align: center;
    color: var(--secondary-color)
}
</style>
