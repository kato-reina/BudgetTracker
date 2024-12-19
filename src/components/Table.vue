<script setup lang="ts">
  import { ref } from 'vue';

  const props = defineProps<{
    tableMessage: string;
    tableData: TableRow[];
    // selectedRow: TableRow | null;
  }>();
  type TableRow = {
    key: number;
    day: string;
    food: number | null;
    fixed: number | null;
  };
  const commonTableHeaderStyle = 'py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm';
  const commonTableDataStyle = 'py-2 px-4 border-b border-gray-20';

  const selectedIndex = ref<number | null>(null);
  // const selectedRow = ref<TableRow>({ key: 0, day: '', food: null, fixed: null });
  const selectedRow = ref<TableRow | null>(null);

  function selectRow(row: TableRow, index: number) {
    selectedIndex.value = index;
    if (selectedRow.value === null) {
      selectedRow.value = row;
    } else {
      selectedRow.value.key = row.key;
      selectedRow.value.day = row.day;
      selectedRow.value.food = row.food;
      selectedRow.value.fixed = row.fixed;
    }
  }
</script>

<template>
  <div class="w-full">
    <span class="text-gray-700 text-lg font-semibold mb-4 block">{{ props.tableMessage }}</span>
    <div v-if="selectedRow">
      <p>Selected Row:</p>
      <p>Key: {{ selectedRow.key }}</p>
      <p>Day: {{ selectedRow.day }}</p>
      <p>Food: {{ selectedRow.food }}</p>
      <p>Fixed: {{ selectedRow.fixed }}</p>
    </div>
    <div class="text-center"><p class="mx-auto">4月</p></div>
    <table class="w-[800px] bg-white border border-gray-20">
      <tr>
        <th :class="commonTableHeaderStyle">日付</th>
        <th :class="commonTableHeaderStyle">曜日</th>
        <th :class="commonTableHeaderStyle">食費</th>
        <th :class="commonTableHeaderStyle">固定費</th>
      </tr>
      <tr
        v-for="(row, index) in props.tableData"
        :key="row.key"
        :class="[commonTableDataStyle, { 'bg-gray-300': selectedIndex === index }]"
        @click="selectRow(row, index)"
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
