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

  // table 4*10
  const rows = 4;
  const tableData = ref<TableRow[]>(
    Array.from({ length: rows }).map((_, rowIndex) => {
      const baseValue = rowIndex + 1;
      return {
        key: baseValue,
        row1: baseValue,
        row2: baseValue + rows,
        row3: baseValue + 2 * rows,
        row4: baseValue + 3 * rows,
        row5: baseValue + 4 * rows,
        row6: baseValue + 5 * rows,
        row7: baseValue + 6 * rows,
        row8: baseValue + 7 * rows,
        row9: baseValue + 8 * rows,
        row10: baseValue + 9 * rows,
      };
    })
  );
  const filteredProps = (row: TableRow) => Object.keys(row).filter((prop) => prop !== 'key');
</script>

<template>
  <div>
    <span class="text-gray-700 text-lg font-semibold mb-4 block">{{ props.tableMessage }}</span>
    <table class="min-w-full bg-white">
      <tr>
        <th v-for="n in 10" :key="n" class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">
          {{ `カテゴリ${n}` }}
        </th>
      </tr>
      <tr v-for="row in tableData" :key="row.key" class="hover:bg-gray-100">
        <td v-for="prop in filteredProps(row)" :key="prop" class="py-2 px-4 border-b border-gray-200">
          {{ row[prop as keyof TableRow] }}
        </td>
      </tr>
    </table>
  </div>
</template>

<style scoped></style>
