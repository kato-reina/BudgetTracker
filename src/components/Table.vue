<script setup lang="ts">
  const props = defineProps<{
    tableMessage: string;
    tableData: TableRow[];
    selectedRow: TableRow | null;
    updateSelectedRow: (row: TableRow) => void;
    tableRowStyle: string[];
  }>();
  type TableRow = {
    key: number;
    day: string;
    food: number | null;
    fixed: number | null;
  };
  const commonTableHeaderStyle = 'py-2 px-4 bg-orange-200 text-gray-600 font-bold uppercase text-sm';
  const commonTableDataStyle = 'text-center py-2 px-4 border-b border-orange-100';

  const colorTableRow = (index: number) => {
    if (index % 7 === 0) {
      return props.tableRowStyle[0];
    } else if (index % 7 === 1) {
      return props.tableRowStyle[1];
    } else {
      return props.tableRowStyle[2];
    }
  };
</script>

<template>
  <div class="w-full m-4">
    <span class="text-gray-700 text-lg font-semibold mb-4">{{ props.tableMessage }}</span>
    <div class="m-4"><p class="mx-auto text-left text-lg font-bold">4月</p></div>
    <table class="w-[800px] bg-white border border-orange-100">
      <tr>
        <th :class="commonTableHeaderStyle">日付</th>
        <th :class="commonTableHeaderStyle">曜日</th>
        <th :class="commonTableHeaderStyle">食費</th>
        <th :class="commonTableHeaderStyle">固定費</th>
      </tr>
      <tr
        v-for="(row, index) in props.tableData"
        :key="row.key"
        :class="colorTableRow(index)"
        @click="updateSelectedRow(row)"
      >
        <td :class="commonTableDataStyle">{{ row.key }}</td>
        <td :class="commonTableDataStyle">{{ row.day }}</td>
        <td :class="commonTableDataStyle">{{ row.food }}</td>
        <td :class="commonTableDataStyle">{{ row.fixed }}</td>
      </tr>
    </table>
  </div>
</template>

<style scoped></style>
