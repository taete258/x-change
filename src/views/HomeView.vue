<template>
  <div class="text-black overflow-auto item-center justify-center p-5">
    <!-- {{ JSON.stringify(dataStates) }} -->
    <MarketPrice
      v-if="!isLoading"
      :dataSymbol="dataStates.symbols"
      :dataTicker="dataStates.ticker"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, onUnmounted, reactive, ref } from "vue";
import { symbols } from "../type/crypto.type";
import MarketPrice from "../components/MarketPrice.vue";
import axios from "axios";
interface dataState {
  symbols: symbols[];
  ticker: any;
}
export default defineComponent({
  components: {
    MarketPrice,
  },
  setup() {
    const baseUrl = "https://api.bitkub.com/";
    const dataStates = reactive<dataState>({
      symbols: [],
      ticker: {},
    });
    const isLoading = ref<boolean>(false);
    let interval: any = null;
    const getCurrentTicker = async () => {
      await axios
        .get(`${baseUrl}api/market/ticker`)
        .then((response) => {
          dataStates.ticker = response.data;
        })
        .catch((e) => alert(e));
    };
    const getSymbols = async () => {
      await axios
        .get(`${baseUrl}/api/market/symbols`)
        .then((response) => {
          dataStates.symbols = response.data.result;
        })
        .catch((e) => alert(e));
    };

    onMounted(async () => {
      isLoading.value = true;
      await getCurrentTicker();
      await getSymbols();
      isLoading.value = false;
      interval = setInterval(async () => {
        await getCurrentTicker();
      }, 10000);
    });

    onUnmounted(() => {
      clearInterval(interval);
    });

    return {
      isLoading,
      baseUrl,
      dataStates,
    };
  },
});
</script>
