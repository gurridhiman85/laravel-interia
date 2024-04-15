<script setup>
    import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
    import Checkbox from '@/Components/Checkbox.vue';
    import GuestLayout from '@/Layouts/GuestLayout.vue';
    import InputError from '@/Components/InputError.vue';
    import InputLabel from '@/Components/InputLabel.vue';
    import PrimaryButton from '@/Components/PrimaryButton.vue';
    import TextInput from '@/Components/TextInput.vue';
    import {Head, Link, useForm} from '@inertiajs/vue3';

    defineProps({
        status: {
            type: String,
        },
    });

    const form = useForm({
        name: '',
        email: '',
        domain_name: '',
        password: '',
        password_confirmation: ''
    });

    const submit = () => {
        form.post(route('tenants.store'), {
            onFinish: () => form.reset('password'),
        });
    };
</script>

<template>
    <AuthenticatedLayout>
        <Head title="Create Tenant"/>

        <section>
            <div class="py-12">
                <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 space-y-6">
                    <div class="p-4 sm:p-8 bg-white shadow sm:rounded-lg">
                        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
                            {{ status }}
                        </div>

                        <form @submit.prevent="submit" class="mt-6 space-y-6">
                            <div>
                                <InputLabel for="name" value="Name"/>

                                <TextInput
                                        id="name"
                                        type="text"
                                        class="mt-1 block w-full"
                                        v-model="form.name"
                                        required
                                        autofocus
                                        autocomplete="name"
                                />

                                <InputError class="mt-2" :message="form.errors.name"/>
                            </div>

                            <div class="mt-4">
                                <InputLabel for="email" value="Email"/>

                                <TextInput
                                        id="email"
                                        type="email"
                                        class="mt-1 block w-full"
                                        v-model="form.email"
                                        required
                                        autocomplete="username"
                                />

                                <InputError class="mt-2" :message="form.errors.email"/>
                            </div>

                            <div class="mt-4">
                                <InputLabel for="domain_name" value="Domain Name"/>

                                <TextInput
                                        id="domain_name"
                                        type="text"
                                        class="mt-1 block w-full"
                                        v-model="form.domain_name"
                                        required
                                        autocomplete="domain_name"
                                />

                                <InputError class="mt-2" :message="form.errors.email"/>
                            </div>

                            <div class="mt-4">
                                <InputLabel for="password" value="Password"/>

                                <TextInput
                                        id="password"
                                        type="password"
                                        class="mt-1 block w-full"
                                        v-model="form.password"
                                        required
                                        autocomplete="new-password"
                                />

                                <InputError class="mt-2" :message="form.errors.password"/>
                            </div>

                            <div class="mt-4">
                                <InputLabel for="password_confirmation" value="Confirm Password"/>

                                <TextInput
                                        id="password_confirmation"
                                        type="password"
                                        class="mt-1 block w-full"
                                        v-model="form.password_confirmation"
                                        required
                                        autocomplete="new-password"
                                />

                                <InputError class="mt-2" :message="form.errors.password_confirmation"/>
                            </div>


                            <div class="flex items-center justify-end mt-4">

                                <PrimaryButton class="ms-4" :class="{ 'opacity-25': form.processing }"
                                               :disabled="form.processing">
                                    Create
                                </PrimaryButton>
                            </div>
                        </form>
                    </div>

                </div>
            </div>
        </section>

    </AuthenticatedLayout>
</template>
