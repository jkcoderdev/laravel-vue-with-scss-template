<script setup>
import { computed } from 'vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({
    href: {
        type: String,
        required: true,
    },
    active: {
        type: Boolean,
    },
});

const isActive = computed(() => props.active);
</script>

<template>
    <Link :href="href" class="link" :class="{ active: isActive }">
        <slot />
    </Link>
</template>

<style lang="scss" scoped>
.link {
    display: block;

    width: 100%;

    padding: 0.5rem 0;
    padding-inline-start: 0.75rem;
    padding-inline-end: 1rem;

    text-align: start;
    font-size: 1rem;
    line-height: 1.5rem;
    font-weight: 500;

    background-color: transparent;
    border: 0;
    border-left: 4px solid transparent;

    transition-property: color, border-color, background-color;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 0.15s;

    &.active {
        border-left: 4px solid #818cf8;
        background-color: #eef2ff;
    }
}
</style>
