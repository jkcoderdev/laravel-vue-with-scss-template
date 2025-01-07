<script setup>
import { onMounted, ref } from 'vue';

const model = defineModel({
    type: String,
    required: true,
});

const input = ref(null);

onMounted(() => {
    if (input.value.hasAttribute('autofocus')) {
        input.value.focus();
    }
});

defineExpose({ focus: () => input.value.focus() });
</script>

<template>
    <input
        v-model="model"
        ref="input"
    />
</template>

<style lang="scss" scoped>
input {
    border-radius: 0.375rem;
    border: 1px solid #d1d5db;
    box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
    background-color: transparent;
    padding: 0 0.25rem;
    line-height: 2rem;

    &:focus {
        border: 1px solid #6366f1;
        outline: none;
    }
}
</style>
