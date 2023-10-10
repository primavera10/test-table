<template>
  <UContainer>
    <UTable :rows="data.posts" :columns="columns"/>
  </UContainer>
</template>

<script setup lang="ts">
  const { data } = await useFetch('https://dummyjson.com/posts');

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
