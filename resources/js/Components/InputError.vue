<script setup>
defineProps({
    message: {
        type: String,
    },
});
</script>

<template>
    <div v-show="message">
        <p>
            {{ message }}
        </p>
    </div>
</template>

<style lang="scss" scoped>
p {
    font-size: 0.875rem;
    line-height: 1.25rem;

    color: #dc2626;
}
</style>