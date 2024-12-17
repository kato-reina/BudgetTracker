<script setup lang="ts">
  const props = defineProps<{
    tableMessage: string;
    tableData: TableRow[];
  }>();

  type TableRow = {
    key: number;
    day: string;
    food: number | null;
    fixed: number | null;
  };
</script>

<template>
  <div>
    <span class="text-gray-700 text-lg font-semibold mb-4 block">{{ props.tableMessage }}</span>
    <div class="text-center"><p class="mx-auto">4月</p></div>
    <table class="min-w-full bg-white">
      <tr>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">日付</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">曜日</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">食費</th>
        <th class="py-2 px-4 bg-gray-200 text-gray-600 font-bold uppercase text-sm">固定費</th>
      </tr>
      <tr v-for="row in props.tableData" :key="row.key" class="hover:bg-gray-100">
        <td class="py-2 px-4 border-b border-gray-200">{{ row.key }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.day }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.food }}</td>
        <td class="py-2 px-4 border-b border-gray-200">{{ row.fixed }}</td>
      </tr>
    </table>
  </div>
</template>

<style scoped></style>
