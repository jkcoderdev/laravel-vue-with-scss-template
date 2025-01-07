<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, useForm } from '@inertiajs/vue3';

defineProps({
    status: {
        type: String,
    },
});

const form = useForm({
    email: '',
});

const submit = () => {
    form.post(route('password.email'));
};
</script>

<template>
    <GuestLayout>
        <Head title="Forgot Password" />

        <div class="text">
            Forgot your password? No problem. Just let us know your email
            address and we will email you a password reset link that will allow
            you to choose a new one.
        </div>

        <div
            v-if="status"
            class="status"
        >
            {{ status }}
        </div>

        <form @submit.prevent="submit">
            <div>
                <InputLabel for="email" value="Email" />

                <TextInput
                    id="email"
                    type="email"
                    class="input"
                    v-model="form.email"
                    required
                    autofocus
                    autocomplete="username"
                />

                <InputError class="error" :message="form.errors.email" />
            </div>

            <div>
                <PrimaryButton
                    :class="{ 'disabled': form.processing }"
                    :disabled="form.processing"
                >
                    Email Password Reset Link
                </PrimaryButton>
            </div>
        </form>
    </GuestLayout>
</template>

<style lang="scss" scoped>
.text {
    margin-bottom: 1rem;

    font-size: 0.875rem;
    line-height: 1.25rem;

    color: #4b5563;
}

.status {
    margin-bottom: 1rem;

    font-size: 0.875rem;
    line-height: 1.25rem;

    font-weight: 500;

    color: #16a34a;
}

form {
    display: flex;
    flex-direction: column;
    gap: 1rem;

    .input {
        margin-top: 0.25rem;
        width: 100%;
        display: block;
    }

    .error {
        margin-top: 0.5rem;
    }

    & > div:last-child {
        display: flex;
        align-items: center;
        justify-content: flex-end;
    }

    .disabled {
        opacity: 0.25;
    }
}
</style>
