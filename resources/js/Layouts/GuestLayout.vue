<script setup>
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import { Link } from '@inertiajs/vue3';
</script>

<template>
    <div class="wrapper">
        <div>
            <Link href="/">
                <ApplicationLogo class="logo" />
            </Link>
        </div>

        <div class="container">
            <slot />
        </div>
    </div>
</template>

<style lang="scss" scoped>
.wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;

    min-height: 100vh;

    padding-top: 1.5rem;

    background-color: #f3f4f6;
}

.logo {
    width: 5rem;
    height: 5rem;

    fill: currentColor;
    color: #6b7280;
}

.container {
    width: 100%;

    margin-top: 1.5rem;
    padding: 1rem 1.5rem;

    overflow: hidden;

    background-color: #ffffff;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.1);
}

@media (min-width: 640px) {
    .wrapper {
        justify-content: center;
        padding-top: 0;
    }

    .container {
        max-width: 28rem;
        border-radius: 0.5rem;
    }
}
</style>