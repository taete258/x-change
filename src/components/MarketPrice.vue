<template>
  <div class="flex flex-col h-[350px]">
    <div class="flex-grow overflow-auto">
      <table class="relative w-full border">
        <thead class="h-[50px] rounded">
          <tr>
            <th
              class="sticky top-[-2px] rounded-tl-lg min-w-[130px] px-6 py-3 text-xs font-medium leading-4 tracking-wider text-left text-gray-100 uppercase border-b border-gray-200 bg-gray-800"
            >
              สกุลเงิน
            </th>
            <th
              class="sticky top-[-2px] min-w-[130px] px-6 py-3 text-xs font-medium leading-4 tracking-wider text-left text-gray-100 uppercase border-b border-gray-200 bg-gray-800"
            >
              ราคาล่าสุด (THB)
            </th>
            <th
              class="sticky top-[-2px] min-w-[130px] px-6 py-3 text-xs font-medium leading-4 tracking-wider text-left text-gray-100 uppercase border-b border-gray-200 bg-gray-800"
            >
              ซื้อขาย/ วัน
            </th>
            <th
              class="sticky top-[-2px] min-w-[130px] px-6 py-3 text-xs font-medium leading-4 tracking-wider text-left text-gray-100 uppercase border-b border-gray-200 bg-gray-800"
            >
              สูงสุด/วัน (THB)
            </th>
            <th
              class="sticky top-[-2px] rounded-tr-lg min-w-[130px] px-6 py-3 text-xs font-medium leading-4 tracking-wider text-left text-gray-100 uppercase border-b border-gray-200 bg-gray-800"
            >
              ต่ำสุด/วัน (THB)
            </th>
          </tr>
        </thead>
        <tbody class="bg-white">
          <tr v-for="(item, index) in dataStates.symbols" :key="index">
            <td class="px-6 py-4 whitespace-no-wrap border-b border-gray-200">
              <div class="flex items-center">
                <div class="flex items-center flex-shrink-0 w-10 h-10">
                  <img
                    class="w-[25px] h-[25px] rounded-full"
                    :src="getCoinIconUrl(item.symbol)"
                    alt="coin icon"
                  />
                </div>

                <div class="ml-1">
                  <div class="text-sm text-left font-medium text-gray-900">
                    {{ item.symbol.split("_")[1] }}
                  </div>
                </div>
              </div>
            </td>

            <td class="px-6 py-4 whitespace-no-wrap border-b border-gray-200">
              <span
                class="float-left inline-flex py-1 px-2 text-xs font-semibold rounded-full"
                :class="[
                  dataStates.ticker[item.symbol]?.percentChange > 0
                    ? 'text-green-700'
                    : 'text-red-700',
                  dataStates.ticker[item.symbol]?.percentChange > 0
                    ? 'bg-green-100'
                    : 'bg-red-100',
                ]"
                >{{
                  dataStates.ticker[item.symbol]?.last.toLocaleString() || 0
                }}
                ({{
                  dataStates.ticker[item.symbol]?.percentChange.toFixed(2) || 0
                }}
                %)</span
              >
            </td>

            <td class="px-6 py-4 whitespace-no-wrap border-b border-gray-200">
              <div class="text-sm text-left font-medium text-gray-900">
                {{
                  dataStates.ticker[item.symbol]?.baseVolume.toLocaleString() ||
                  0
                }}

                {{ item.symbol.split("_")[1] }}
              </div>
            </td>

            <td
              class="px-6 py-4 text-gray-500 whitespace-no-wrap border-b border-gray-200"
            >
              <div class="text-sm text-left font-medium text-gray-900">
                {{
                  dataStates.ticker[item.symbol]?.high24hr.toLocaleString() || 0
                }}
              </div>
            </td>
            <td
              class="px-6 py-4 text-gray-500 whitespace-no-wrap border-b border-gray-200"
            >
              <div class="text-sm text-left font-medium text-gray-900">
                {{
                  dataStates.ticker[item.symbol]?.low24hr.toLocaleString() || 0
                }}
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, onUpdated, reactive } from "vue";
import { symbols } from "../type/crypto.type";

interface dataState {
  symbols: symbols[];
  ticker: any;
}

export default defineComponent({
  props: ["dataSymbol", "dataTicker"],
  setup(props) {
    const dataStates = reactive<dataState>({
      symbols: [],
      ticker: {},
    });

    const getCoinIconUrl = (item: string) => {
      return `https://cdn.bitkubnow.com/coins/icon/${item.split("_")[1]}.png`;
    };

    onMounted(() => {
      dataStates.symbols = props.dataSymbol;
      dataStates.ticker = props.dataTicker;
    });

    onUpdated(() => {
      dataStates.ticker = props.dataTicker;
    });

    return {
      dataStates,
      getCoinIconUrl,
    };
  },
});
</script>
