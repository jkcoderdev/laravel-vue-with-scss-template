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

const classes = computed(() =>
    props.active
        ? 'block w-full ps-3 pe-4 py-2 border-l-4 border-indigo-400 text-start text-base font-medium text-indigo-700 bg-indigo-50 focus:outline-none focus:text-indigo-800 focus:bg-indigo-100 focus:border-indigo-700 transition duration-150 ease-in-out'
        : 'block w-full ps-3 pe-4 py-2 border-l-4 border-transparent text-start text-base font-medium text-gray-600 hover:text-gray-800 hover:bg-gray-50 hover:border-gray-300 focus:outline-none focus:text-gray-800 focus:bg-gray-50 focus:border-gray-300 transition duration-150 ease-in-out',
);

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
