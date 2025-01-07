<script setup>
import { Link } from '@inertiajs/vue3';

defineProps({
    href: {
        type: String,
        required: true,
    },
});
</script>

<template>
    <Link
        :href="href"
        class="link"
    >
        <slot />
    </Link>
</template>

<style lang="scss" scoped>
.link {
    display: block;
    
    width: 100%;

    padding: 0.5rem 1rem;

    text-align: start;
    font-size: 0.875rem;
    line-height: 1.25rem;

    background-color: transparent;
    color: #374151;
    border: none;

    transition-property: background-color;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 0.15s;

    &:hover, &:focus {
        background-color: #f3f4f6;
    }

    &:focus {
        outline: 2px solid transparent;
        outline-offset: 2px;
    }
}
</style>
