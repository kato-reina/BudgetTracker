<script setup lang="ts">
  import Form from '@/components/Form.vue';
  import Table from '@/components/Table.vue';
  import { ref } from 'vue';

  const formMessage = '家計簿をつける';
  const tableMessage = '一覧を表示します';
  const sideMenuMessage = 'My家計簿';

  // for form component
  // 今回はtrueでForm表示
  const pageSelect = ref(true);
  const setPageSelect = (flag: boolean) => (pageSelect.value = flag);

  // for table component
  type TableRow = {
    key: number;
    day: string;
    food: number | null;
    fixed: number | null;
  };

  const days = ['土', '日', '月', '火', '水', '木', '金'];

  const otherDaysStyle = 'hover:bg-gray-200';
  const saturdayStyle = 'bg-blue-200 hover:bg-blue-300';
  const sundaysStyle = 'bg-red-200 hover:bg-red-300';

  const tableRowStyle = [saturdayStyle, sundaysStyle, otherDaysStyle];
  const tableData = ref<TableRow[]>(
    Array.from({ length: 30 }).map((_, index) => ({
      key: index + 1,
      day: days[index % 7],
      food: null,
      fixed: null,
    }))
  );

  const selectedRow = ref<TableRow | null>(null);
  const updateSelectedRow = (row: TableRow) => {
    if (selectedRow.value === null) {
      selectedRow.value = { ...row };
    } else {
      selectedRow.value.key = row.key;
      selectedRow.value.day = row.day;
      selectedRow.value.food = row.food;
      selectedRow.value.fixed = row.fixed;
    }
    setPageSelect(true);
  };

  // for main css
  const commonButtonStyle =
    'w-[200px] text-white font-bold py-2 px-4 border-b-4 active:border-none active:translate-y-1 rounded h-12';
  const formButtonStyle = `bg-blue-500 hover:bg-blue-400 active:bg-blue-600 border-blue-700 hover:border-blue-500 ${commonButtonStyle}`;
  const tableButtonStyle = `bg-green-500 hover:bg-green-400 active:bg-green-600 border-green-700 hover:border-green-500 ${commonButtonStyle}`;
</script>

<template>
  <div class="w-[1500px] flex">
    <div class="bg-gray-300">
      <span class="text-gray-700 font-bold">{{ sideMenuMessage }}</span>
      <div class="m-4">
        <button :class="formButtonStyle" @click="setPageSelect(true)">記録</button>
      </div>
      <div class="m-4">
        <button :class="tableButtonStyle" @click="setPageSelect(false)">確認</button>
      </div>
    </div>
    <div class="m-4">
      <Form v-if="pageSelect" :formMessage="formMessage" :tableData="tableData" :selectedRow="selectedRow" />
      <Table
        v-else
        :tableMessage="tableMessage"
        :tableData="tableData"
        :selectedRow="selectedRow"
        :updateSelectedRow="updateSelectedRow"
        :tableRowStyle="tableRowStyle"
      />
    </div>
  </div>
</template>

<style scoped></style>
