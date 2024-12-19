<script setup lang="ts">
  const props = defineProps<{
    tableMessage: string;
    tableData: TableRow[];
    selectedRow: TableRow | null;
    updateSelectedRow: (row: TableRow) => void;
  }>();
  type TableRow = {
    key: number;
    day: string;
    food: number | null;
    fixed: number | null;
  };
  const commonTableHeaderStyle = 'py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm';
  const commonTableDataStyle = 'py-2 px-4 border-b border-gray-20';
</script>

<template>
  <div class="w-full">
    <span class="text-gray-700 text-lg font-semibold mb-4 block">{{ props.tableMessage }}</span>
    <div class="text-center"><p class="mx-auto">4月</p></div>
    <table class="w-[800px] bg-white border border-gray-20">
      <tr>
        <th :class="commonTableHeaderStyle">日付</th>
        <th :class="commonTableHeaderStyle">曜日</th>
        <th :class="commonTableHeaderStyle">食費</th>
        <th :class="commonTableHeaderStyle">固定費</th>
      </tr>
      <tr v-for="row in props.tableData" :key="row.key" class="hover:bg-gray-100" @click="updateSelectedRow(row)">
        <td :class="commonTableDataStyle">{{ row.key }}</td>
        <td :class="commonTableDataStyle">{{ row.day }}</td>
        <td :class="commonTableDataStyle">{{ row.food }}</td>
        <td :class="commonTableDataStyle">{{ row.fixed }}</td>
      </tr>
    </table>
  </div>
</template>

<style scoped></style>
