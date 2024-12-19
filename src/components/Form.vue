<script setup lang="ts">
  import { defineProps, ref, watch } from 'vue';

  type TableRow = {
    key: number;
    day: string;
    food: number | null;
    fixed: number | null;
  };

  const props = defineProps<{
    formMessage: string;
    tableData: TableRow[];
    selectedRow: TableRow | null;
  }>();

  const selectedYear = ref('');
  const selectedMonth = ref('');
  const selectedDay = ref('');
  const selectedCategory = ref('');
  const inputText = ref('');

  const optionsOfYear = [2024];
  const optionsOfMonth = [4];
  const optionsOfDay = [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31,
  ];
  const optionsOfCategory = ['食費', '固定費'];

  const formErrorMessage = ref('');

  const updateTable = () => {
    const updateYear = parseInt(selectedYear.value, 10);
    const updateMonth = parseInt(selectedMonth.value, 10);
    const updateDay = parseInt(selectedDay.value, 10);
    const updateValue = parseInt(inputText.value, 10);

    if (isItemsSelected(updateYear, updateMonth, selectedCategory.value, updateDay)) {
      formErrorMessage.value = '年、月、日、カテゴリをすべて選択してください';
    } else if (isNaN(updateValue)) {
      formErrorMessage.value = '金額を数字で入力して下さい';
    } else {
      updateTableData(updateDay, selectedCategory.value, updateValue);
      formErrorMessage.value = '';
      inputText.value = '';
    }
  };

  const isItemsSelected = (year: number, month: number, category: string, day: number) => {
    return isNaN(year) || isNaN(month) || category === '' || isNaN(day);
  };

  const updateTableData = (day: number, category: string, value: number) => {
    if (category === '食費') {
      props.tableData[day - 1].food = value;
    } else if (category === '固定費') {
      props.tableData[day - 1].fixed = value;
    }
  };

  // selectedRowが変更されたときにプルダウンの値を更新
  watch(
    () => props.selectedRow,
    (newRow) => {
      if (newRow) {
        updateSelectedValues(newRow);
      }
    },
    { immediate: true }
  );

  function updateSelectedValues(row: TableRow) {
    selectedYear.value = '2024';
    selectedMonth.value = '4';
    selectedDay.value = row.key.toString();
  }
</script>

<template>
  <div class="w-[800px] max-w-md bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
    <span class="text-gray-700 text-lg font-semibold mb-4 block">{{ props.formMessage }}</span>
    <div class="flex">
      <div class="flex m-4 space-x-1">
        <select v-model="selectedYear" class="p-2 border rounded bg-white shadow">
          <option disabled value="" selected>年</option>
          <option v-for="option in optionsOfYear" :key="option" :value="option">{{ option }}</option>
        </select>

        <select v-model="selectedMonth" class="p-2 border rounded bg-white shadow">
          <option disabled value="" selected>月</option>
          <option v-for="option in optionsOfMonth" :key="option" :value="option">{{ option }}</option>
        </select>

        <select v-model="selectedDay" class="p-2 border rounded bg-white shadow">
          <option disabled value="" selected>日</option>
          <option v-for="option in optionsOfDay" :key="option" :value="option">{{ option }}</option>
        </select>
      </div>
      <div class="m-4 space-x-4">
        <select v-model="selectedCategory" class="p-2 border rounded bg-white shadow">
          <option disabled value="" selected>カテゴリ</option>
          <option v-for="option in optionsOfCategory" :key="option" :value="option">{{ option }}</option>
        </select>
      </div>
    </div>
    <div class="flex items-center mt-4">
      <form class="flex-grow">
        <input
          v-model="inputText"
          class="shadow appearance-none border-2 border-gray-500 rounded w-full py-2 px-3 text-gray-700 leading-tight"
          type="text"
          placeholder="入力してください"
        />
      </form>
      <button
        class="ml-4 bg-orange-500 hover:bg-orange-400 active:bg-orange-600 text-white font-bold py-2 px-4 border-b-4 border-orange-700 hover:border-orange-500 active:border-none active:translate-y-1 rounded h-12"
        @click="updateTable"
      >
        送信
      </button>
    </div>
    <span class="text-red-700 text-lg font-semibold mb-4 block">{{ formErrorMessage }}</span>
  </div>
</template>

<style scoped></style>
