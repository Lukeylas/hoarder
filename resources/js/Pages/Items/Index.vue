<template>
    <Head title="Items" />

    <AuthenticatedLayout>
        <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
            <form @submit.prevent="form.post(route('items.store'), { onSuccess: () => form.reset() })">
                <input
                    type="text"
                    v-model="form.name"
                    placeholder="What new item did you hoard?"
                    class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
                ></input>
                <InputError :message="form.errors.message" class="mt-2" />
                <PrimaryButton class="mt-4">Add Item</PrimaryButton>
            </form>

            <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
                <ListItem v-for="item in items" :key="item.id" :item="item"></ListItem>
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<script setup>
    // Layout
    import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
    // Components
    import ListItem from '@/Components/ListItem.vue';
    import InputError from '@/Components/InputError.vue';
    import PrimaryButton from '@/Components/PrimaryButton.vue';
    import { useForm, Head } from '@inertiajs/vue3';
    
    defineProps(['items']);

    const form = useForm({
        name: '',
    });
</script>