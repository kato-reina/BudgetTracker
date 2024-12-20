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

  const otherDaysStyle = 'hover:bg-green-100';
  const saturdayStyle = 'bg-blue-100 hover:bg-blue-200';
  const sundaysStyle = 'bg-red-100 hover:bg-red-200';

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
  const formButtonStyle = `bg-orange-500 hover:bg-orange-400 active:bg-orange-600 border-orange-700 hover:border-orange-500 ${commonButtonStyle}`;
  const tableButtonStyle = `bg-green-500 hover:bg-green-400 active:bg-green-600 border-green-700 hover:border-green-500 ${commonButtonStyle}`;
</script>

<template>
  <div class="flex w-full h-[1500px]">
    <div class="bg-yellow-50 mx-auto items-center">
      <div class="ml-20 mt-3">
        <h1 class="text-gray-700 font-bold">{{ sideMenuMessage }}</h1>
      </div>
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
