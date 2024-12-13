<script setup lang="ts">
  import { ref } from 'vue';

  const props = defineProps<{
    tableMessage: string;
  }>();

  type TableRow = {
    key: number;
    row1: number;
    row2: number;
    row3: number;
    row4: number;
    row5: number;
    row6: number;
    row7: number;
    row8: number;
    row9: number;
    row10: number;
  };

  const tableData = ref<TableRow[]>([
    { key: 1, row1: 10, row2: 20, row3: 30, row4: 40, row5: 50, row6: 60, row7: 70, row8: 80, row9: 90, row10: 100 },
    { key: 2, row1: 15, row2: 25, row3: 35, row4: 45, row5: 55, row6: 65, row7: 75, row8: 85, row9: 95, row10: 105 },
    { key: 3, row1: 20, row2: 30, row3: 40, row4: 50, row5: 60, row6: 70, row7: 80, row8: 90, row9: 100, row10: 110 },
    { key: 4, row1: 25, row2: 35, row3: 45, row4: 55, row5: 65, row6: 75, row7: 85, row8: 95, row9: 105, row10: 115 },
  ]);
</script>

<template>
  <div>
    <span class="text-gray-700 text-lg font-semibold mb-4 block">{{ props.tableMessage }}</span>
    <table class="min-w-full bg-white">
      <tr>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">row1</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">row2</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">row3</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">row4</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">row5</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">row6</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">row7</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">row8</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">row9</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">row10</th>
      </tr>
      <tr v-for="row in tableData" :key="row.key" class="hover:bg-gray-100">
        <td class="py-2 px-4 border-b border-gray-200">{{ row.row1 }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.row2 }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.row3 }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.row4 }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.row5 }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.row6 }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.row7 }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.row8 }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.row9 }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.row10 }}</td>
      </tr>
    </table>
  </div>
</template>

<style scoped></style>
