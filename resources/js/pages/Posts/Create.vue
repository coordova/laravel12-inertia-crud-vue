<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head, Link, useForm } from '@inertiajs/vue3';
import InputError from '@/components/InputError.vue';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';
import { LoaderCircle } from 'lucide-vue-next';

// Breadcrumbs
const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Post Create',
        href: '/posts/create',
    },
];

const form = useForm({
    title: '',
    body: '',
});

const submit = () => {
    form.post(route('posts.store'), {
        preserveScroll: true,
        onSuccess: () => {
            form.reset();
        },
        onError: () => {
            form.reset();
        },
        onFinish: () => {
            form.reset();
        },

    });
};

</script>

<template>
    <Head title="Post Create" />
    
    <AppLayout :breadcrumbs="breadcrumbs">
        <div class="flex h-full flex-1 flex-col gap-4 rounded-xl p-4">
        <!-- Create a Post Button -->
        <div>
            <Link
                :href="route('posts.index')"
                class="rounded-sm bg-gray-700 px-3 py-2 text-xs font-medium text-white hover:bg-gray-800 focus:ring-4 focus:ring-gray-300 focus:outline-none dark:bg-gray-600 dark:hover:bg-gray-700 dark:focus:ring-gray-800"
            >
                Go Back
            </Link>
        </div>
            <div class="overflow-x-auto">
                <form @submit.prevent="submit">
                    <div class="grid gap-2">
                        <Label for="email">Title</Label>
                        <Input
                            id="title"
                            type="text"
                            class="mt-1 block w-full"
                            v-model="form.title"
                            placeholder="Title"
                        />
                        <InputError class="mt-2" :message="form.errors.title" />
                    </div>
                    <div class="grid gap-2">
                        <Label for="email">Body</Label>
                        <Input
                            id="body"
                            type="text"
                            class="mt-1 block w-full"
                            v-model="form.body"
                            placeholder="Body"
                        />
                        <InputError class="mt-2" :message="form.errors.body" />
                    </div>
                    <div class="flex items-center gap-4">
                        <Button :disabled="form.processing">
                            <LoaderCircle v-if="form.processing" class="h-4 w-4 animate-spin" />
                            Save
                        </Button>
                    </div>
                </form>
            </div>
        </div>
    </AppLayout>
</template>