<script setup lang="ts">
import InputError from '@/components/InputError.vue';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head, Link, useForm } from '@inertiajs/vue3';
import { LoaderCircle } from 'lucide-vue-next';

// Breadcrumbs
const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Post Edit',
        href: '/posts/edit',
    },
];

// definir las props
/* const props = defineProps({
    // post: Object, // sin necesidad de usar la interface Post
    post: Object<Post>(),
}); */

const props = defineProps(['post']);

const form = useForm({
    title: props.post.title,
    body: props.post.body,
});

const submit = () => {
    form.put(route('posts.update', props.post.id), {
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
    <Head title="Post Edit" />

    <AppLayout :breadcrumbs="breadcrumbs">
        <div class="flex h-full flex-1 flex-col gap-4 rounded-xl p-4">
            <!-- Go Back Button -->
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
                        <Input id="title" type="text" class="mt-1 block w-full" v-model="form.title" placeholder="Title" />
                        <InputError class="mt-2" :message="form.errors.title" />
                    </div>
                    <div class="my-4 grid gap-2">
                        <Label for="email">Body</Label>
                        <textarea
                            id="body"
                            class="file:text-foreground placeholder:text-muted-foreground selection:bg-primary selection:text-primary-foreground dark:bg-input/30 border-input mt-1 block h-15 w-full min-w-0 rounded-md border bg-transparent px-3 py-1 text-base shadow-xs transition-[color,box-shadow] outline-none file:inline-flex file:h-7 file:border-0 file:bg-transparent file:text-sm file:font-medium disabled:pointer-events-none disabled:cursor-not-allowed disabled:opacity-50 md:text-sm"
                            v-model="form.body"
                            placeholder="Body"
                        ></textarea>
                        <InputError class="mt-2" :message="form.errors.body" />
                    </div>
                    <div class="flex items-center gap-4">
                        <Button :disabled="form.processing">
                            <LoaderCircle v-if="form.processing" class="h-4 w-4 animate-spin" />
                            Update
                        </Button>
                    </div>
                </form>
            </div>
        </div>
    </AppLayout>
</template>
