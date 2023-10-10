<template>
  <UContainer v-if="data">
    <UTable
      :rows="data.posts"
      :columns="columns"
      :loading="pending"
      :loading-state="{ icon: 'i-heroicons-arrow-path-20-solid', label: 'Loading...' }"
    >
      <template #tags-data="{ row }">
        <UBadge v-for="tag in row.tags" :key="tag" class="ml-2">{{ tag }}</UBadge>
      </template>
    </UTable>
    <UPagination v-model="page" :page-count="pageCount" :total="data.total" />
  </UContainer>
</template>

<script setup lang="ts">
  const page = ref(1);
  const pageCount = 10;

  const { data, pending } = await useFetch('https://dummyjson.com/posts', {
    query: {
      limit: pageCount,
      skip: computed(() => (page.value - 1) * pageCount),
    }
  });

  const columns = [{
    key: 'id',
    label: 'Id'
  },
    {
      key: 'title',
      label: 'Title',
    },
    {
      key: 'tags',
      label: 'Tags'
    },
    {
      key: 'reactions',
      label: 'Reactions'
    }
  ];
</script>
