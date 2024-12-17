<script setup lang="ts">
  import Form from '@/components/Form.vue';
  import Table from '@/components/Table.vue';
  import { ref } from 'vue';

  const formMessage = 'フォームからメッセージ送信';
  const tableMessage = '一覧を表示します';
  const pageSelect = ref(true);

  const SwitchToForm = () => {
    pageSelect.value = true;
  };

  const switchToTable = () => {
    pageSelect.value = false;
  };

  type TableRow = {
    key: number;
    day: string;
    food: number | null;
    fixed: number | null;
  };

  const tableData = ref<TableRow[]>([
    { key: 1, day: '土', food: null, fixed: null },
    { key: 2, day: '日', food: null, fixed: null },
    { key: 3, day: '月', food: null, fixed: null },
    { key: 4, day: '火', food: null, fixed: null },
    { key: 5, day: '水', food: null, fixed: null },
    { key: 6, day: '木', food: null, fixed: null },
    { key: 7, day: '金', food: null, fixed: null },
    { key: 8, day: '土', food: null, fixed: null },
    { key: 9, day: '日', food: null, fixed: null },
    { key: 10, day: '月', food: null, fixed: null },
    { key: 11, day: '火', food: null, fixed: null },
    { key: 12, day: '水', food: null, fixed: null },
    { key: 13, day: '木', food: null, fixed: null },
    { key: 14, day: '金', food: null, fixed: null },
    { key: 15, day: '土', food: null, fixed: null },
    { key: 16, day: '日', food: null, fixed: null },
    { key: 17, day: '月', food: null, fixed: null },
    { key: 18, day: '火', food: null, fixed: null },
    { key: 19, day: '水', food: null, fixed: null },
    { key: 20, day: '木', food: null, fixed: null },
    { key: 21, day: '金', food: null, fixed: null },
    { key: 22, day: '土', food: null, fixed: null },
    { key: 23, day: '日', food: null, fixed: null },
    { key: 24, day: '月', food: null, fixed: null },
    { key: 25, day: '火', food: null, fixed: null },
    { key: 26, day: '水', food: null, fixed: null },
    { key: 27, day: '木', food: null, fixed: null },
    { key: 28, day: '金', food: null, fixed: null },
    { key: 29, day: '土', food: null, fixed: null },
    { key: 30, day: '日', food: null, fixed: null },
  ]);
</script>

<template>
  <div class="w-[800px] h-[600px]">
    <div class="flex">
      <div class="m-4">
        <button
          class="bg-blue-500 hover:bg-blue-400 active:bg-blue-600 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 active:border-none active:translate-y-1 rounded h-12"
          @click="SwitchToForm"
        >
          Formを表示
        </button>
      </div>
      <div class="m-4">
        <button
          class="bg-green-500 hover:bg-green-400 active:bg-green-600 text-white font-bold py-2 px-4 border-b-4 border-green-700 hover:border-green-500 active:border-none active:translate-y-1 rounded h-12"
          @click="switchToTable"
        >
          Tableを表示
        </button>
      </div>
    </div>
    <div class="m-4">
      <Form v-if="pageSelect" :formMessage="formMessage" :tableData="tableData" />
      <Table v-else :tableMessage="tableMessage" :tableData="tableData" />
    </div>
  </div>
</template>

<style scoped></style>
