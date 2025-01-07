<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, useForm } from '@inertiajs/vue3';

const form = useForm({
    password: '',
});

const submit = () => {
    form.post(route('password.confirm'), {
        onFinish: () => form.reset(),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Confirm Password" />

        <div class="text">
            This is a secure area of the application. Please confirm your
            password before continuing.
        </div>

        <form @submit.prevent="submit">
            <div>
                <InputLabel for="password" value="Password" />
                <TextInput
                    id="password"
                    type="password"
                    class="input"
                    v-model="form.password"
                    required
                    autocomplete="current-password"
                    autofocus
                />
                <InputError class="error" :message="form.errors.password" />
            </div>

            <div>
                <PrimaryButton
                    class="submit-button"
                    :class="{ 'disabled': form.processing }"
                    :disabled="form.processing"
                >
                    Confirm
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
        justify-content: flex-end;
    }

    .submit-button {
        margin-inline-start: 1rem;

        &.disabled {
            opacity: 0.25;
        }
    }
}
</style>
