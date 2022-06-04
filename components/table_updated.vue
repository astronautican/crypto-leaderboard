<template>
  <div class="flex items-center justify-center min-h-screen bg-gray-900">
    <div class="col-span-12">
      <div class="header flex justify-center">
        <div class="my-50">
          <h1>Crypto Leaderboard</h1>
        </div>
      </div>
      <div class="overflow-auto lg:overflow-visible">
        <table class="table text-gray-400 border-separate space-y-6 text-sm">
          <thead class="bg-gray-800 text-gray-500">
            <tr>
              <!-- <th class="p-3">Image</th> -->
              <th class="p-3">Coin</th>
              <th class="p-3 text-left">Names</th>
              <th class="p-3 text-left">Price</th>
              <th class="p-3 text-left">24h Changes</th>
              <th class="p-3 text-left">ATH</th>
              <th class="p-3 text-left">ATL</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in DataDump" :key="item" class="bg-gray-800">
              <td class="p-3">#{{ item.market_cap_rank }}</td>

              <td class="p-3">
                <div class="flex align-items-center">
                  <img
                    class="rounded-full h-12 w-12 object-cover"
                    :src="item.image"
                    alt="unsplash image"
                  />
                  <div class="ml-5">
                    <h2>{{ item.symbol }}</h2>
                  </div>
                </div>
              </td>
              <td class="p-3">{{ item.name }}</td>
              <td class="p-3 font-bold">${{ item.current_price }}</td>
              <td class="p-3">
                <span class="bg-green-400 text-gray-50 rounded-md px-2">{{
                  item.price_change_percentage_24h
                }}</span>
              </td>
              <td class="p-3">
                <i class="material-icons-outlined text-base">{{
                  item.ath_change_percentage
                }}</i>
              </td>
              <td>
                <i class="material-icons-outlined text-base">{{
                  item.atl_change_percentage
                }}</i>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Table",
  data: function () {
    return {
      DataDump: [],
    };
  },

  created() {
    // Simple GET request using fetch
    fetch(
      "https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false"
    )
      .then((response) => response.json())
      .then((data) => (this.DataDump = data));
  },
};
</script>

<style>
.table {
  border-spacing: 0 15px;
}

i {
  font-size: 1rem !important;
}

.table tr {
  border-radius: 20px;
}

tr td:nth-child(n + 5),
tr th:nth-child(n + 5) {
  border-radius: 0 0.625rem 0.625rem 0;
}

tr td:nth-child(1),
tr th:nth-child(1) {
  border-radius: 0.625rem 0 0 0.625rem;
}
</style>