<template>
    <UContainer>
      <div v-if="checkDataArr">
        <UTable  v-if="dataArr" :rows="dataArr.posts"></UTable>
      </div>
    </UContainer>
</template>

<script setup lang="ts">

  import { onMounted } from "vue";

  let dataArr;

  onMounted(async () => {
    const data = await fetch('https://dummyjson.com/posts')
    dataArr = await data.json()

    console.log(dataArr)
  })

  function checkDataArr(){
    return !!dataArr;
  }

</script>
