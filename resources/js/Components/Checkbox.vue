<script setup>
import { computed } from 'vue';

const emit = defineEmits(['update:checked']);

const props = defineProps({
    checked: {
        type: [Array, Boolean],
        required: true,
    },
    value: {
        default: null,
    },
});

const proxyChecked = computed({
    get() {
        return props.checked;
    },

    set(val) {
        emit('update:checked', val);
    },
});
</script>

<template>
    <input
        type="checkbox"
        :value="value"
        v-model="proxyChecked"
        class="rounded border-gray-300 text-indigo-600 shadow-sm focus:ring-indigo-500"
    />
</template>

<style lang="scss" scoped>
input[type='checkbox'] {
    border-radius: 0.25rem;
    border-color: #d1d5db;
    color: #4f46e5;
    box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
}
</style>
