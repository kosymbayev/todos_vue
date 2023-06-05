<template>
    <header class="header">
        <span class="logo">TODOS</span>
    </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'TheHeader',
});
</script>

<style>
.header {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 1.6rem;
}

.logo {
    font-size: 2.4rem;
    font-weight: 500;
    color: var(--primary-color)
}
</style>
