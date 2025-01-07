<script setup>
import { computed } from 'vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const props = defineProps({
    status: {
        type: String,
    },
});

const form = useForm({});

const submit = () => {
    form.post(route('verification.send'));
};

const verificationLinkSent = computed(
    () => props.status === 'verification-link-sent',
);
</script>

<template>
    <GuestLayout>
        <Head title="Email Verification" />

        <div class="text">
            Thanks for signing up! Before getting started, could you verify your
            email address by clicking on the link we just emailed to you? If you
            didn't receive the email, we will gladly send you another.
        </div>

        <div
            class="status"
            v-if="verificationLinkSent"
        >
            A new verification link has been sent to the email address you
            provided during registration.
        </div>

        <form @submit.prevent="submit">
            <div>
                <PrimaryButton
                    :class="{ 'disabled': form.processing }"
                    :disabled="form.processing"
                >
                    Resend Verification Email
                </PrimaryButton>

                <Link
                    :href="route('logout')"
                    method="post"
                    as="button"
                    class="link"
                    >Log Out</Link
                >
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

form > div {
    margin-top: 1rem;

    display: flex;
    align-items: center;
    justify-content: space-between;

    .disabled {
        opacity: 0.25;
    }

    .link {
        border-radius: 0.375rem;

        font-size: 0.875rem;
        line-height: 1.25rem;

        text-decoration: underline;

        color: #4b5563;

        &:hover {
            color: #111827;
        }

        &:focus {
            outline: 2px solid transparent;
            outline-offset: 2px;

            box-shadow: 0 0 0 2px #ffffff, 0 0 0 4px #6366f1;
        }
    }
}
</style>
