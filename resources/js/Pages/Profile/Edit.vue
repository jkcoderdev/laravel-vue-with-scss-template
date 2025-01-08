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
            <h2>
                Profile
            </h2>
        </template>

        <div class="page">
            <div class="content">
                <div
                    class="card"
                >
                    <UpdateProfileInformationForm
                        :must-verify-email="mustVerifyEmail"
                        :status="status"
                        class="card-content"
                    />
                </div>

                <div
                    class="card"
                >
                    <UpdatePasswordForm class="card-content" />
                </div>

                <div
                    class="card"
                >
                    <DeleteUserForm class="card-content" />
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<style lang="scss" scoped>
.page{
    padding: 3rem;

    .header{

        h2{
            font-size: 1.25rem;
            line-height: 1.75rem;
            font-weight: 600;
            line-height: 1.25rem;
            color: #333;
        }

        
    }

    .content{

        margin: 1.5rem auto;
        padding-left: 1.5rem;
        padding-right: 1.5rem;

        max-width: 80rem;

        @media (min-width: 640px) {
            padding-left: 1.5rem;
            padding-right: 1.5rem;
        }

        @media (min-width: 1024px) {
            padding-left: 2rem;
            padding-right: 2rem;
        }

        .card{
            background-color: white;
            padding: 1rem;
            box-shadow: 0 20px 25px -5px rgb(0, 0, 0, 0.1), 0 8px 10px -6px rgb(0, 0, 0, 0.1);

            @media (min-width: 640px) {
                border-radius: 0.5rem;
                padding: 2rem;
            }

            .card-content{
                max-width: 36rem;
            }
        }

    } 

    
}
</style>
