<template>
  <div style="position: relative">
    <!-- <button
      style="margin-left: -850px; position: sticky; top: 50px"
      @click="getPost()"
    >
      تحديث
    </button> -->

    <div
      class="items-center mt-5"
      v-for="(currency, index) in post"
      :key="currency.second_currency"
      style="border-top-left-radius: 20px; border-top-right-radius: 20px"
    >
      <NewCalculator
        :index_id="index"
        style="margin: 10px"
        :currency_price_active="currency"
      />
    </div>
    <button
      style="margin-left: -850px; position: sticky; top: 100px"
      @click="deleteall()"
    >
      ترقيم جديد
    </button>
  </div>
</template>

<script>
import NewCalculator from "./components/NewCalc.vue";
import PrintPage from "./components/print.vue";
function convertTimestampToDate(timestamp) {
  const date = new Date(timestamp);
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, "0");
  const day = String(date.getDate()).padStart(2, "0");
  return `${year}-${month}-${day}`;
}
function convertTimestampToTime(timestamp) {
  const date = new Date(timestamp);
  const hours = String(date.getHours()).padStart(2, "0");
  const minutes = String(date.getMinutes()).padStart(2, "0");
  const seconds = String(date.getSeconds()).padStart(2, "0");
  return `${hours}:${minutes}:${seconds}`;
}
const priceArray = [
  {
    currency_buy_code: "TYR",
    currency_buy_name: "الليرة التركية",
    currency_selling_code: "USD",
    currency_selling_name: "دولار",
    currency_selling_price: "00",
    currency_buy_price: "00",
    last_update_date: convertTimestampToDate(Date.now()),
    last_update_time: convertTimestampToTime(Date.now()),
  },
  {
    currency_buy_code: "SYP",
    currency_buy_name: "الليرة السورية",
    currency_selling_code: "TYR",
    currency_selling_name: "الليرة التركية",
    currency_selling_price: "00",
    currency_buy_price: "00",
    last_update_date: convertTimestampToDate(Date.now()),
    last_update_time: convertTimestampToTime(Date.now()),
},
{
    currency_buy_code: "SYP",
    currency_buy_name: "الليرة السورية",
    currency_selling_code: "USD",
    currency_selling_name: "دولار",
    currency_selling_price: "00",
    currency_buy_price: "00",
    last_update_date: convertTimestampToDate(Date.now()),
    last_update_time: convertTimestampToTime(Date.now()),
},
{
  currency_buy_code: "EUR",
  currency_buy_name: "اليورو",
  currency_selling_code: "USD",
  currency_selling_name: "دولار",
  currency_selling_price: "00",
  currency_buy_price: "00",
  last_update_date: convertTimestampToDate(Date.now()),
  last_update_time: convertTimestampToTime(Date.now()),
},
];
export default {
  components: {
    NewCalculator,
    PrintPage,
  },
  data() {
    return {
      post: {},
    };
  },
  methods: {
    getPost() {
      this.post = priceArray;
      //   fetch("https://alnoorexchange.com/api/v1/currency-price")
      //     .then((Response) => Response.json())
      //     .then((data) => (this.post = priceArray));
    },
    deleteall() {
      localStorage.clear();
    },
  },
  mounted() {
    this.getPost();
  },
};
</script>
