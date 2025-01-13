<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header class="header">
            <h2>Dashboard</h2>
        </template>

        <div class="content py-12">
            <div class="section">
                <div class="text">
                    You're logged in!
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<style lang="scss" scoped>
.header h2 {
    font-size: 1.25rem;
    line-height: 1.25;
    font-weight: 600;
    color: #1f2937;
}

.content {
    max-width: 80rem;

    padding: 3rem 0;
    margin: 0 auto;

    @media (min-width: 640px) {
        padding-left: 1.5rem;
        padding-right: 1.5rem;
    }

    @media (min-width: 1024px) {
        padding-left: 2rem;
        padding-right: 2rem;
    }

    .section {
        overflow: hidden;

        padding: 1.5rem;

        background-color: #ffffff;

        box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
        
        @media (min-width: 640px) {
            border-radius: 0.5rem;
        }

        .text {
            color: #111827;
        }
    }
}
</style>
