<script setup lang="ts">
  import Form from '@/components/Form.vue';
  import Table from '@/components/Table.vue';
  import { ref } from 'vue';

  const formMessage = 'フォームからメッセージ送信';
  const tableMessage = '一覧を表示します';
  const pageSelect = ref(true);
  // 今回はtrueでForm表示
  const setPageSelect = (flag: boolean) => (pageSelect.value = flag);
  // for css
  const commonButtonStyle =
    'text-white font-bold py-2 px-4 border-b-4 active:border-none active:translate-y-1 rounded h-12';
  const fromButtonStyle = `bg-blue-500 hover:bg-blue-400 active:bg-blue-600 border-blue-700 hover:border-blue-500 ${commonButtonStyle}`;
  const tableButtonStyle = `bg-green-500 hover:bg-green-400 active:bg-green-600 border-green-700 hover:border-green-500 ${commonButtonStyle}`;
</script>

<template>
  <div class="w-[1000px] h-[600px]">
    <div class="flex">
      <div class="m-4">
        <button :class="fromButtonStyle" @click="setPageSelect(true)">Formを表示</button>
      </div>
      <div class="m-4">
        <button :class="tableButtonStyle" @click="setPageSelect(false)">Tableを表示</button>
      </div>
    </div>
    <div class="m-4">
      <Form v-if="pageSelect" :formMessage="formMessage" />
      <Table v-else :tableMessage="tableMessage" />
    </div>
  </div>
</template>

<style scoped></style>
