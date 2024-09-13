<script setup>
import DangerButton from '@/Components/DangerButton.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import Modal from '@/Components/Modal.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { useForm } from '@inertiajs/vue3';
import { nextTick, onMounted, ref } from 'vue';
import { useModal } from '@/Composables/useModal';

const modal = ref(null);
const passwordInput = ref(null);

onMounted(() => {
    modal.value = useModal('#userId');
});

const form = useForm({
    password: '',
});

const confirmUserDeletion = () => {
    modal.value.show();

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
    modal.value.hide();

    form.reset();
};

onMounted(() => {
    closeModal();
})
</script>

<template>
    <section class="space-y-6">
        <header>
            <h2 class="text-lg font-medium text-gray-900">Delete Account</h2>

            <p class="mt-1 text-sm text-gray-600">
                Once your account is deleted, all of its resources and data will be permanently deleted. Before deleting
                your account, please download any data or information that you wish to retain.
            </p>
        </header>

        <DangerButton @click="confirmUserDeletion">Delete Account</DangerButton>

        <Modal id="userId" @close="closeModal">
            <template #title>
                <h2 class="text-lg font-medium text-gray-900">
                    Are you sure you want to delete your account?
                </h2>
            </template>

            <p class="mt-1 text-sm text-gray-600">
                Once your account is deleted, all of its resources and data will be permanently deleted. Please
                enter your password to confirm you would like to permanently delete your account.
            </p>

            <template #body>
                <InputLabel for="password" value="Password" class="sr-only" />

                <TextInput id="password" ref="passwordInput" v-model="form.password" type="password"
                    class="form-control" placeholder="Password" @keyup.enter="deleteUser" />

                <InputError :message="form.errors.password" class="mt-2" />
            </template>

            <template #footer>
                <SecondaryButton @click="closeModal"> Cancel </SecondaryButton>

                <DangerButton class="ms-3" :class="{ 'opacity-25': form.processing }" :disabled="form.processing"
                    @click="deleteUser">
                    Delete Account
                </DangerButton>
            </template>
        </Modal>
    </section>
</template>
