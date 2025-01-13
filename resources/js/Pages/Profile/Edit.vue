<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import DeleteUserForm from './Partials/DeleteUserForm.vue';
import UpdatePasswordForm from './Partials/UpdatePasswordForm.vue';
import UpdateProfileInformationForm from './Partials/UpdateProfileInformationForm.vue';
import { Head } from '@inertiajs/vue3';

defineProps({
    mustVerifyEmail: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});
</script>

<template>
    <Head title="Profile" />

    <AuthenticatedLayout>
        <template #header class="header">
            <h2>Profile</h2>
        </template>

        <div class="content">
            <div class="section">
                <UpdateProfileInformationForm
                    :must-verify-email="mustVerifyEmail"
                    :status="status"
                />
            </div>

            <div class="section">
                <UpdatePasswordForm />
            </div>

            <div class="section">
                <DeleteUserForm />
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

    display: flex;
    flex-direction: column;
    gap: 1.5rem;

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

        padding: 1rem;

        background-color: #ffffff;

        box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.05), 0 1px 2px -1px rgba(0, 0, 0, 0.1);
        
        @media (min-width: 640px) {
            padding: 2rem;
            border-radius: 0.5rem;
        }

        & > * {
            max-width: 36rem;
        }
    }
}
</style>
