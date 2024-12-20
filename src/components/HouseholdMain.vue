<script setup lang="ts">
  import Form from '@/components/Form.vue';
  import Table from '@/components/Table.vue';
  import { ref } from 'vue';

  const formMessage = '家計簿をつける';
  const tableMessage = '一覧を表示します';

  // for side menu
  const sideMenuTopMessage = '家計簿を';
  const sideMenuBottomMessage = 'する';
  const commonSideMenuStyle = 'mx-4 text-gray-900 font-bold';
  const SideMenuTopStyle = `${commonSideMenuStyle} mt-4 text-left`;
  const SideMenuBottomStyle = `${commonSideMenuStyle} mb-4 text-right`;

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

  const otherDaysStyle = 'hover:bg-orange-100';
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
    'w-[40%] text-black font-bold py-2 px-4 border-b-4 active:border-none active:translate-y-1 rounded h-12 mx-auto my-1';
  const formButtonStyle = `bg-orange-200 hover:bg-orange-100 active:bg-orange-200 border-orange-300 hover:border-orange-200 ${commonButtonStyle}`;
  const tableButtonStyle = `bg-orange-200 hover:bg-orange-100 active:bg-orange-200 border-orange-300 hover:border-orange-200 ${commonButtonStyle}`;
</script>

<template>
  <div class="flex w-screen h-[1000px]">
    <div class="flex flex-col w-[15%] h-[200px]">
      <h1 :class="SideMenuTopStyle">{{ sideMenuTopMessage }}</h1>
      <button :class="formButtonStyle" @click="setPageSelect(true)">更新</button>
      <button :class="tableButtonStyle" @click="setPageSelect(false)">確認</button>
      <h1 :class="SideMenuBottomStyle">{{ sideMenuBottomMessage }}</h1>
    </div>
    <div>
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
