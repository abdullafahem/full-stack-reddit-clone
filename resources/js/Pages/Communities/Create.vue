<template>
    <Head title="Create Community" />

    <BreezeAuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Create Community
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="max-w-md bg-white m-2 p-6 mx-auto">
                    <form @submit.prevent="submit">
                        <div>
                            <BreezeLabel for="name" value="Name" />
                            <BreezeInput
                                id="name"
                                type="text"
                                class="mt-1 block w-full"
                                v-model="form.name"
                                autofocus
                                autocomplete="name"
                            />
                            <BreezeInputError :message="errors.name" />
                        </div>

                        <div>
                            <BreezeLabel for="slug" value="Slug" />
                            <BreezeInput
                                id="slug"
                                type="text"
                                class="mt-1 block w-full"
                                v-model="form.slug"
                                autocomplete="slug"
                            />
                            <BreezeInputError :message="errors.slug" />
                        </div>

                        <div class="mt-4">
                            <BreezeLabel
                                for="description"
                                value="Description"
                            />
                            <BreezeInput
                                id="description"
                                type="text"
                                class="mt-1 block w-full"
                                v-model="form.description"
                                autocomplete="description"
                            />
                            <BreezeInputError :message="errors.description" />
                        </div>

                        <div class="flex items-center justify-end mt-4">
                            <BreezeButton
                                class="ml-4"
                                :class="{ 'opacity-25': form.processing }"
                                :disabled="form.processing"
                            >
                                Store
                            </BreezeButton>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>

<script setup>
import BreezeAuthenticatedLayout from "@/Layouts/Authenticated.vue";
import { Head, useForm } from "@inertiajs/inertia-vue3";
import BreezeButton from "@/Components/Button.vue";
import BreezeInput from "@/Components/Input.vue";
import BreezeInputError from "@/Components/InputError.vue";
import BreezeLabel from "@/Components/Label.vue";

defineProps({
    errors: Object,
});

const form = useForm({
    name: "",
    description: "",
    slug: "",
});

const submit = () => {
    form.post(route("communities.store"), {
        onFinish: () => form.reset("name", "description", "slug"),
    });
};
</script>
