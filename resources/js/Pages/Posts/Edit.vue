<script setup>
import BreezeAuthenticatedLayout from "@/Layouts/Authenticated.vue";
import { Head } from "@inertiajs/inertia-vue3";
import { Link } from "@inertiajs/inertia-vue3";
import { reactive } from "vue";
import { Inertia } from "@inertiajs/inertia";

const props = defineProps({
    post: Object,
});

const form = reactive({
    title: props.post.title,
    description: props.post.description,
});

function submit() {
    Inertia.post(`/posts/${props.post.id}`, {
        _method: "put",
        title: form.title,
        description: form.description,
    });
}
</script>

<template>
    <Head title="Edit-Post" />

    <BreezeAuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Edit posts
            </h2>
        </template>
        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <div class="mb-4">
                            <Link
                                class="px-6 py-2 mb-2 bg-green-500 rounded"
                                :href="route('posts.home')"
                                >Back</Link
                            >
                        </div>
                        <div class="p-6 bg-white border-b border-gray-200">
                            <form @submit.prevent="submit">
                                <div>
                                    <label for="title">Title</label>
                                    <input
                                        type="text"
                                        v-model="form.title"
                                        class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600"
                                    />
                                </div>
                                <div class="mt-4">
                                    <label for="title">Description</label>
                                    <textarea
                                        name="description"
                                        type="text"
                                        v-model="form.description"
                                        class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600"
                                    >
                                    </textarea>
                                </div>

                                <!-- submit -->
                                <div class="flex items-center mt-4">
                                    <button
                                        class="px-6 py-2 text-white bg-gray-900 rounded"
                                    >
                                        Update
                                    </button>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>
