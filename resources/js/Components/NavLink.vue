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
