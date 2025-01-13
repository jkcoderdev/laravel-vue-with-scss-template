<script setup>
import DangerButton from '@/Components/DangerButton.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import Modal from '@/Components/Modal.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { useForm } from '@inertiajs/vue3';
import { nextTick, ref } from 'vue';

const confirmingUserDeletion = ref(false);
const passwordInput = ref(null);

const form = useForm({
    password: '',
});

const confirmUserDeletion = () => {
    confirmingUserDeletion.value = true;

    nextTick(() => passwordInput.value.focus());
};

const deleteUser = () => {
    form.delete(route('profile.destroy'), {
        preserveScroll: true,
        onSuccess: () => closeModal(),
        onError: () => passwordInput.value.focus(),
        onFinish: () => form.reset(),
    });
};

const closeModal = () => {
    confirmingUserDeletion.value = false;

    form.clearErrors();
    form.reset();
};
</script>

<template>
    <section>
        <header class="text-box">
            <h2>
                Delete Account
            </h2>

            <p>
                Once your account is deleted, all of its resources and data will
                be permanently deleted. Before deleting your account, please
                download any data or information that you wish to retain.
            </p>
        </header>

        <DangerButton @click="confirmUserDeletion">Delete Account</DangerButton>

        <Modal :show="confirmingUserDeletion" @close="closeModal">
            <div class="modal">
                <div class="text-box">
                    <h2>
                        Are you sure you want to delete your account?
                    </h2>

                    <p>
                        Once your account is deleted, all of its resources and data
                        will be permanently deleted. Please enter your password to
                        confirm you would like to permanently delete your account.
                    </p>
                </div>
                

                <div>
                    <InputLabel
                        for="password"
                        value="Password"
                        class="label"
                    />

                    <TextInput
                        id="password"
                        ref="passwordInput"
                        v-model="form.password"
                        type="password"
                        class="input"
                        placeholder="Password"
                        @keyup.enter="deleteUser"
                    />

                    <InputError :message="form.errors.password" class="error" />
                </div>

                <div class="action-buttons">
                    <SecondaryButton @click="closeModal">
                        Cancel
                    </SecondaryButton>

                    <DangerButton
                        class="danger-btn"
                        :disabled="form.processing"
                        @click="deleteUser"
                    >
                        Delete Account
                    </DangerButton>
                </div>
            </div>
        </Modal>
    </section>
</template>

<style lang="scss" scoped>
section {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 1.5rem;

    .text-box {
        h2 {
            font-size: 1.125rem;
            line-height: 1.75rem;
            font-weight: 500;
            color: #111827;
        }

        p {
            margin-top: 0.25rem;
            font-size: 0.875rem;
            line-height: 1.25rem;
            color: #4b5563;
        }
    }

    .modal {
        padding: 1.5rem;

        display: flex;
        flex-direction: column;
        gap: 1.5rem;

        .label {
            position: absolute;
            width: 1px;
            height: 1px;
            padding: 0;
            margin: -1px;
            overflow: hidden;
            clip: rect(0, 0, 0, 0);
            white-space: nowrap;
            border-width: 0;
        }

        .input {
            width: 75%;
            margin-top: 0.25rem;
            display: block;
        }

        .error {
            margin-top: 0.5rem;
        }

        .action-buttons {
            display: flex;
            justify-content: flex-end;

            .danger-btn {
                margin-inline-start: 0.75rem;

                &:disabled {
                    opacity: 0.25;
                }
            }
        }
    }
}
</style>
