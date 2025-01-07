<script setup>
defineProps({
    value: {
        type: String,
    },
});
</script>

<template>
    <label>
        <span v-if="value">{{ value }}</span>
        <span v-else><slot /></span>
    </label>
</template>

<style lang="scss" scoped>
label {
    display: block;

    font-size: 0.875rem;
    line-height: 1.25rem;

    font-weight: 500;

    color: #374151;
}
</style>
