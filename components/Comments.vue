<template>
  <div v-if="data">
    <div v-for="comment in data.comments" :key="comment.id" class="mb-4">
      <div class="mb-2">
        <UAvatar :alt="comment.user.username" size="sm" class="mr-2" />
        {{ comment.user.username }}
      </div>
      {{ comment.body }}
    </div>
  </div>
</template>

<script setup lang="ts">
  const props = defineProps({
    postId: {
      type: Number,
      required: true,
    },
  });

  interface Comment {
    id: number,
    body: string,
    postId: number,
    user: {
      id: number,
      username: string
    }
  }

  const { data } = useFetch<{ comments: Comment[] }>(`https://dummyjson.com/posts/${props.postId}/comments`);
</script>
