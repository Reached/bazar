<script>
    export default {
        methods: {
            formatDate(date) {
                return date.substr(0, 16).replace('T', ' ');
            }
        }
    }
</script>

<template>
    <layout :title="__('Categories')">
        <card :title="__('Categories')">
            <template #header>
                <inertia-link :href="`${$inertia.page.url}/create`" class="btn btn-primary btn-sm">
                    {{ __('Create Category') }}
                </inertia-link>
            </template>
            <data-table :response="$page.results" :filters="$page.filters" searchable>
                <data-column :label="__('Photo')">
                    <template #default="item">
                        <img
                            class="table-preview-image"
                            :src="item.media[0] ? item.media[0].urls.thumb : '/vendor/bazar/img/placeholder.svg'"
                            :alt="item.name"
                        >
                    </template>
                </data-column>
                <data-column :label="__('Name')" sort="name">
                    <template #default="item">
                        <inertia-link :href="`${$inertia.page.url}/${item.id}`">
                            {{ item.name }}
                        </inertia-link>
                    </template>
                </data-column>
                <data-column :label="__('Created at')" sort="created_at">
                    <template #default="item">
                        {{ formatDate(item.created_at) }}
                    </template>
                </data-column>
            </data-table>
        </card>
    </layout>
</template>
