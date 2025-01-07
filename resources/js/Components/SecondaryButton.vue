<script setup>
defineProps({
    type: {
        type: String,
        default: 'button',
    },
});
</script>

<template>
    <button
        :type="type"
        class="inline-flex items-center rounded-md border border-gray-300 bg-white px-4 py-2 text-xs font-semibold uppercase tracking-widest text-gray-700 shadow-sm transition duration-150 ease-in-out hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 disabled:opacity-25"
    >
        <slot />
    </button>
</template>

<style lang="scss" scoped>
@mixin transition {
    transition-property: color, background-color, box-shadow;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 0.15s;
}

button {
    padding: 0.5rem 1rem;
    
    display: inline-flex;
    align-items: center;
    
    border-radius: 0.375rem;
    
    border: 1px solid #d1d5db;
    background-color: #ffffff;
    color: #374151;

    font-size: 0.75rem;
    line-height: 1rem;
    font-weight: 600;

    text-transform: uppercase;
    letter-spacing: 0.1em;
}
</style>
