<template>
  <UContainer v-if="data">
    <UTable
      @select="select"
      :rows="data.posts"
      :columns="columns"
      :loading="pending"
      :loading-state="{ icon: 'i-heroicons-arrow-path-20-solid', label: 'Loading...' }"
    >
      <template #tags-data="{ row }">
        <UBadge v-for="tag in row.tags" :key="tag" class="ml-2">
          {{ tag }}
        </UBadge>
      </template>
    </UTable>
    <UPagination v-model="page" :page-count="pageCount" :total="data.total"/>
    <UModal v-model="isOpen">
      <UCard :ui="{ divide: 'divide-y divide-gray-100 dark:divide-gray-800' }">
        <template #header>
          {{ selectedItem.title }}
        </template>

        <UFormGroup label="Title">
          <UInput :model-value="selectedItem.title" disabled/>
        </UFormGroup>
        <UFormGroup label="Body" class="mt-4">
          <UTextarea :model-value="selectedItem.body" disabled />
        </UFormGroup>
        <UFormGroup label="Reactions" class="mt-4">
          <UInput :model-value="selectedItem.reactions" disabled />
        </UFormGroup>
        <UFormGroup label="Tags" class="mt-4">
          <UBadge v-for="tag in selectedItem.tags" :key="tag" class="ml-2">
            {{ tag }}
          </UBadge>
        </UFormGroup>
        <template #footer>
          <UButton @click="isOpen = false">
            Close
          </UButton>
        </template>
      </UCard>
    </UModal>
  </UContainer>
</template>

<script setup lang="ts">
  const page = ref(1);
  const pageCount = 10;

  const { data, pending } = await useFetch<{ posts: Array<any> }>('https://dummyjson.com/posts', {
    query: {
      limit: pageCount,
      skip: computed(() => (page.value - 1) * pageCount),
    }
  });

  const isOpen = ref(false);
  const selectedItem = ref();

  function select(row: any) {
    isOpen.value = true;
    selectedItem.value = row;
  }

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
