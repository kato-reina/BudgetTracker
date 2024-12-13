<script setup lang="ts">
  import { defineProps } from 'vue';

  const props = defineProps<{
    formMessage: string;
  }>();
</script>

<template>
  <div class="max-w-md bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
    <span class="text-gray-700 text-lg font-semibold mb-4 block">{{ props.formMessage }}</span>
    <form>
      <input
        class="shadow appearance-none border-2 border-gray-500 rounded w-full py-2 px-3 text-gray-700 leading-tight"
        type="text"
        placeholder="入力してください"
      />
    </form>
  </div>
</template>

<style scoped></style>
