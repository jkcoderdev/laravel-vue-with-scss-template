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
        ? 'inline-flex items-center px-1 pt-1 border-b-2 border-indigo-400 text-sm font-medium leading-5 text-gray-900 focus:outline-none focus:border-indigo-700 transition duration-150 ease-in-out'
        : 'inline-flex items-center px-1 pt-1 border-b-2 border-transparent text-sm font-medium leading-5 text-gray-500 hover:text-gray-700 hover:border-gray-300 focus:outline-none focus:text-gray-700 focus:border-gray-300 transition duration-150 ease-in-out',
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
    display: inline-flex;
    align-items: center;

    padding: 0 0.25rem;
    padding-top: 0.25rem;

    border-bottom: 2px solid transparent;

    font-size: 0.875rem;
    line-height: 1.25rem;

    font-weight: 500;

    color: #6b7280;

    transition-property: color, border-color;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 0.15s;

    &:not(.active):hover,
    &:not(.active):focus {
        border-bottom: 2px solid #d1d5db;
        color: #374151;
    }

    &.active {
        border-bottom: 2px solid #818cf8;
        color: #111827;
    }

    &.active:focus {
        border-bottom: 2px solid #4338ca;
    }

    &:focus {
        outline: 2px solid transparent;
        outline-offset: 2px;
    }
}
</style>
