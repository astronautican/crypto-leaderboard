<!-- Please remove this file from your project -->
<template>
  <div class="flex justify-center">
    <table class="table-auto">
      <thead>
        <tr>
          <th>Song</th>
          <th>Artist</th>
          <th>Year</th>
        </tr>
      </thead>
      <tbody>
        <div v-for="item in DataDump" :key="item">
          <tr>
            <td>{{ item.name }}</td>
            <td>{{ item.symbol }}</td>
            <td>{{ item.symbol }}</td>
          </tr>
        </div>
      </tbody>
    </table>
  </div>
</template>

<script>
// https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false

export default {
  name: "NuxtTutorial",
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
