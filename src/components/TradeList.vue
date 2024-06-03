<template>
    <div>
      <form @submit.prevent="fetchTrades">
        <div>
          <label for="exchange">Exchange:</label>
          <input type="text" id="exchange" v-model="filters.exchange" placeholder="binance" />
        </div>
        <div>
          <label for="date">Date:</label>
          <input type="text" id="date" v-model="filters.date" placeholder="01062024" />
        </div>
        <div>
          <label for="pair">Pair:</label>
          <input type="text" id="pair" v-model="filters.pair" placeholder="btcusdt" />
        </div>
        <button type="submit">Fetch Trades</button>
      </form>
      <ul v-if="filteredTrades.length">
        <li v-for="trade in filteredTrades" :key="trade.TradeID">
          {{ trade.Exchange }} - {{ trade.Pair }} - {{ trade.Price }} - {{ trade.Qty }} - {{ trade.Time }}
        </li>
      </ul>
      <div v-else>No trades found</div>
    </div>
  </template>
  
  <script setup>
  import { reactive, computed } from 'vue';
  
  const filters = reactive({
    exchange: '',
    date: '',
    pair: ''
  });
  
  const trades = reactive([]);
  
  const filteredTrades = computed(() => {
    return trades.filter(trade => {
      return (!filters.exchange || trade.Exchange === filters.exchange) &&
             (!filters.date || trade.Date === filters.date) &&
             (!filters.pair || trade.Pair === filters.pair);
    });
  });
  
  async function fetchTrades() {
    // Mocking the API response
    const response = {
      status: 200,
      data: [
        {
          Exchange: "binance",
          Date: "01062024",
          Pair: "btcusdt",
          TradeID: "1",
          Price: "0.1",
          Qty: "1.0",
          QuoteQty: "0.1",
          Time: "123456789",
          IsBuyerMaker: true,
          IsBestMatch: true
        },
        {
          Exchange: "binance",
          Date: "01062024",
          Pair: "btcusdt",
          TradeID: "2",
          Price: "0.2",
          Qty: "2.0",
          QuoteQty: "0.4",
          Time: "123456790",
          IsBuyerMaker: false,
          IsBestMatch: true
        },
        {
          Exchange: "coinbase",
          Date: "01062024",
          Pair: "ethusdt",
          TradeID: "3",
          Price: "0.3",
          Qty: "3.0",
          QuoteQty: "0.9",
          Time: "123456791",
          IsBuyerMaker: true,
          IsBestMatch: false
        },
        {
          Exchange: "kraken",
          Date: "02062024",
          Pair: "btcusdt",
          TradeID: "4",
          Price: "0.4",
          Qty: "4.0",
          QuoteQty: "1.6",
          Time: "123456792",
          IsBuyerMaker: false,
          IsBestMatch: true
        }
      ]
    };
  
    if (response.status === 200) {
      trades.splice(0, trades.length, ...response.data);
    } else {
      console.error('Error fetching trades');
    }
  }
  </script>
  
  <style scoped>
  form {
    margin-bottom: 20px;
  }
  
  form div {
    margin-bottom: 10px;
  }
  
  button {
    padding: 5px 10px;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    background: #f4f4f4;
    margin: 5px 0;
    padding: 10px;
    border-radius: 4px;
  }
  </style>
  