<template>
  <div class="main-info-container">
    <div class="current-data-container">
      <div class="current-balance-box">
        <span class="title-box"
          ><h2>Current Balance</h2>
          <img src="../assets/icons/dots_icon.svg" alt=""
        /></span>
        <span class="current-price" ref="currentPrice"
          >${{ firstCurrentPrice }}</span
        >
        <span class="last-month-info-up" v-if="firstCurrentPercentMonth > 0"
          ><img src="../assets/icons/arrow_up.svg" alt="" />
          {{ firstCurrentPercentMonth }}% vs last month</span
        >
        <span class="last-month-info-down" v-if="firstCurrentPercentMonth < 0"
          ><img src="../assets/icons/arrow_down.svg" alt="" />
          {{ firstCurrentPercentMonth }}% vs last month</span
        >
        <div class="invest-button-box">
          <button class="violet-button">Quick Invest</button>
          <button class="white-button">Show Report</button>
        </div>
      </div>
      <div class="summary-box" v-if="widthWindow >= 899">
        <span class="title-box"
          ><h2>Summary</h2>
          <img src="../assets/icons/dots_icon.svg" alt=""
        /></span>
        <canvas id="myChart" width="100%" height="100%"></canvas>
      </div>
    </div>
    <div class="others-value-table">
      <ul class="others-value-table-menubar">
        <li class="menubar-options">Summary</li>
        <li class="menubar-options">Table</li>
        <li class="menubar-options">Charts</li>
        <li class="menubar-options">Reporting</li>
        <li class="menubar-options">Analysis</li>
      </ul>
      <ul class="others-crypto" v-if="cryptoCurrency.data != null">
        <li
          class="crypto"
          v-for="(cryptoData, index) in cryptoCurrency.data"
          :key="cryptoData[index]"
        >
          <picture class="crypto-circle"
            ><img class="crypto-logo" :src="cryptoData.logo" alt=""
          /></picture>
          <!-- BTC Name -->
          <span class="btc-box">
            <h3 class="btc">btc</h3>
            <h3 class="crypto-name">{{ cryptoData.name }}</h3>
          </span>
          <!-- Current Price -->
          <span class="current-price-box">
            <h3 class="price">Price</h3>
            <h3 v-show="index <= 1 || index == 3" class="current-balance">
              ${{ CurrentBalance }}
            </h3>
            <h3 v-show="index == 2" class="current-balance">
              ${{ SecondCurrentBalance }}
            </h3>
          </span>
          <!-- Change Precent -->
          <span class="change-precent-box">
            <h3 class="change">Change</h3>
            <h3
              class="change-precent-up"
              v-show="index <= 1 || index == 3"
              v-if="CurrentBalancePercent > 0"
            >
              {{ CurrentBalancePercent }}
              <img src="../assets/icons/arrow_up.svg" alt="" />
            </h3>
            <h3
              class="change-precent-down"
              v-show="index <= 1 || index == 3"
              v-if="CurrentBalancePercent < 0"
            >
              {{ CurrentBalancePercent }}
              <img src="../assets/icons/arrow_down.svg" alt="" />
            </h3>
            <h3
              class="change-precent-up"
              v-show="index == 2"
              v-if="SecondCurrentBalancePercent > 0"
            >
              {{ SecondCurrentBalancePercent }}
              <img src="../assets/icons/arrow_up.svg" alt="" />
            </h3>
            <h3
              class="change-precent-down"
              v-show="index == 2"
              v-if="SecondCurrentBalancePercent < 0"
            >
              {{ SecondCurrentBalancePercent }}
              <img src="../assets/icons/arrow_down.svg" alt="" />
            </h3>
          </span>
          <img
            class="line-up"
            v-show="index <= 1 || index == 3"
            v-if="CurrentBalancePercent > 0"
            src="../assets/icons/line-up.svg"
            alt=""
          />
          <img
            class="line-down"
            v-show="index <= 1 || index == 3"
            v-if="CurrentBalancePercent < 0"
            src="../assets/icons/line-down.svg"
            alt=""
          />
          <img
            class="line-up"
            v-show="index == 2"
            v-if="SecondCurrentBalancePercent > 0"
            src="../assets/icons/line-up.svg"
            alt=""
          />
          <img
            class="line-down"
            v-show="index == 2"
            v-if="SecondCurrentBalancePercent < 0"
            src="../assets/icons/line-down.svg"
            alt=""
          />
          <div class="button-box" v-if="widthWindow >= 899">
            <button class="sell-button">Sell</button>
            <button class="buy-button">Buy</button>
          </div>
        </li>
      </ul>
    </div>
    <div class="summary-box-mobile" v-if="widthWindow < 899">
      <span class="title-box"
        ><h2>Summary</h2>
        <img src="../assets/icons/dots_icon.svg" alt=""
      /></span>
      <canvas id="myChart2" width="100%" height="100%"></canvas>
    </div>
  </div>
</template>

<script>
import Chart from "chart.js/auto";
import axios from "axios";
export default {
  data() {
    return {
      cryptoCurrency: [],
      cryptoMoreData: [],
      firstCurrentPrice: 0,
      firstCurrentPercentMonth: 0,
      firstCurrentPercentLastMonth: 0,
      secondCurrentPrice: 0,
      secondCurrentPercentMonth: 0,
      widthWindow: window.innerWidth,
      heightWindow: window.innerHeight,
    };
  },
  async created() {
    //Get Name and Logo Crypto
    axios
      .get("http://localhost:8080/v1/cryptocurrency/info?&id=1,2,3,4,5", {
        headers: {
          "X-CMC_PRO_API_KEY": "e52d580d-c5e4-48c1-b307-91b707cbd60d",
        },
      })
      .then((response) => (this.cryptoCurrency = response.data));
    //Get Price and Precent Crypto
    axios
      .get(
        "http://localhost:8080/v1/cryptocurrency/category?&id=605e2ce9d41eae1066535f7c",
        {
          headers: {
            "X-CMC_PRO_API_KEY": "e52d580d-c5e4-48c1-b307-91b707cbd60d",
          },
        }
      )
      .then((response) => (this.cryptoMoreData = response.data));
  },
  mounted() {
    axios
      .get(
        "http://localhost:8080/v1/cryptocurrency/category?&id=605e2ce9d41eae1066535f7c",
        {
          headers: {
            "X-CMC_PRO_API_KEY": "e52d580d-c5e4-48c1-b307-91b707cbd60d",
          },
        }
      )
      .then((response) => {
        this.cryptoMoreData = response.data;
        let cryptoData = this.cryptoMoreData.data;
        let cryptoCoins = cryptoData.coins[0];
        let coinsValues = cryptoCoins.quote;
        console.log(coinsValues);
        this.firstCurrentPercentLastMonth =
          coinsValues.USD.percent_change_30d.toFixed(2);
        //Value current price vs last month
        let currentPrice = coinsValues.USD.price.toFixed(2);
        let percent60 = coinsValues.USD.percent_change_60d.toFixed(2);
        let currentPriceTwoMonthAgo = currentPrice / percent60;
        let currentPriceLastMonth = (
          currentPrice / this.firstCurrentPercentLastMonth
        ).toFixed(2);
        const month = [
          "January",
          "February",
          "March",
          "April",
          "May",
          "June",
          "July",
          "August",
          "September",
          "October",
          "November",
          "December",
        ];

        const currentDate = new Date();
        let currentMonth = month[currentDate.getMonth()];
        let lastMonth = month[currentDate.getMonth() - 1];
        let lastMonth60 = month[currentDate.getMonth() - 2];
        const dataMonth = [
          { month: lastMonth60, price: currentPriceTwoMonthAgo },
          { month: lastMonth, price: currentPriceLastMonth },
          { month: currentMonth, price: currentPrice },
        ];
        const diagram = document.querySelector("#myChart");
        const diagram2 = document.querySelector("#myChart2");
        const data = {
          labels: dataMonth.map((row) => row.month),
          datasets: [
            {
              label: "Bitcoin current price during three months",
              data: dataMonth.map((row) => row.price),
              fill: true,
              borderColor: "rgb(75, 192, 192)",
              tension: 0.5,
            },
          ],
        };
        const config = {
          type: "line",
          data: data,
        };
        new Chart(diagram, config);
        new Chart(diagram2, config);
      });
    this.$nextTick(() => {
      window.addEventListener("resize", this.onResize);
    });
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.onResize);
  },
  methods: {
    onResize(e) {
      this.widthWindow = window.innerWidth;
      this.heightWindow = window.innerHeight;
    },
  },
  computed: {
    CurrentBalance() {
      let cryptoData = this.cryptoMoreData.data;
      let cryptoCoins = cryptoData.coins[0];
      let coinsValues = cryptoCoins.quote;
      //console.log(coinsValues.USD);
      this.firstCurrentPrice = coinsValues.USD.price.toFixed(2);

      return this.firstCurrentPrice;
    },
    CurrentBalancePercent() {
      let cryptoData = this.cryptoMoreData.data;
      let cryptoCoins = cryptoData.coins[0];
      let coinsValues = cryptoCoins.quote;
      this.firstCurrentPercentMonth =
        coinsValues.USD.percent_change_1h.toFixed(2) -
        coinsValues.USD.percent_change_30d.toFixed(2);
      return this.firstCurrentPercentMonth;
    },
    SecondCurrentBalance() {
      let cryptoData = this.cryptoMoreData.data;
      let cryptoCoins = cryptoData.coins[6];
      let coinsValues = cryptoCoins.quote;
      //console.log(coinsValues.USD);
      this.secondCurrentPrice = coinsValues.USD.price.toFixed(2);
      return this.secondCurrentPrice;
    },
    SecondCurrentBalancePercent() {
      let cryptoData = this.cryptoMoreData.data;
      let cryptoCoins = cryptoData.coins[6];
      let coinsValues = cryptoCoins.quote;
      this.secondCurrentPercentMonth =
        coinsValues.USD.percent_change_30d.toFixed(2);
      //console.log(coinsValues.USD.percent_change_30d.toFixed(2));
      return this.secondCurrentPercentMonth;
    },
  },
};
</script>

<style lang="scss">
.main-info-container {
  display: flex;
  flex-direction: column;
  .current-data-container {
    margin-top: 5rem;
    display: flex;
    justify-content: space-between;
    @media screen and (max-width: 899px) {
      flex-direction: column;
      align-items: center;
    }
    .current-balance-box {
      background: #f7f7f9;
      border-radius: 16px;
      width: 509px;
      height: 336px;
      display: flex;
      flex-direction: column;
      padding: 1rem;
      @media screen and (max-width: 1114px) {
        width: 450px;
      }
      @media screen and (max-width: 1004px) {
        width: 400px;
      }
      @media screen and (max-width: 899px) {
        margin-bottom: 2rem;
        width: 80%;
      }
      @media screen and (max-width: 600px) {
        width: 100%;
      }
      .title-box {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding-left: 1rem;
        padding-right: 1rem;
        width: 100%;
        height: 3rem;
        img {
          width: 16px;
        }
      }
      .current-price {
        margin-left: 1rem;
        margin-top: 3rem;
        color: #9896a1;
        font-style: normal;
        font-weight: 300;
        font-size: 56px;
        line-height: 56px;
      }
      .last-month-info-up {
        display: flex;
        align-items: center;
        margin-top: 1rem;
        margin-left: 1rem;
        font-weight: 500;
        font-size: 18px;
        line-height: 24px;
        color: #2dc78f;
        img {
          margin-right: 0.5rem;
        }
      }
      .last-month-info-down {
        display: flex;
        align-items: center;
        margin-top: 1rem;
        margin-left: 1rem;
        font-weight: 500;
        font-size: 18px;
        line-height: 24px;
        color: #ea4d4d;
        img {
          margin-right: 0.5rem;
        }
      }
    }
    .summary-box {
      background: #f7f7f9;
      border-radius: 16px;
      width: 509px;
      height: 336px;
      padding: 1rem;
      display: flex;
      flex-direction: column;
      @media screen and (max-width: 1114px) {
        width: 450px;
      }
      @media screen and (max-width: 1004px) {
        width: 400px;
      }
      .title-box {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding-left: 1rem;
        padding-right: 1rem;
        padding-top: 0.8rem;
        width: 100%;
        height: 3rem;
        img {
          width: 16px;
        }
      }
      #myChart {
        padding: 1.5rem;
        @media screen and (max-width: 1004px) {
          padding: 1rem;
        }
      }
    }
  }
  .others-value-table {
    border-radius: 16px;
    width: 100%;
    min-height: 350px;
    background: #f7f7f9;
    margin-top: 2.3rem;
    padding: 2rem;
    position: relative;
    @media screen and (max-width: 899px) {
      height: 350px;
      overflow: hidden;
    }
    @media screen and (max-width: 563px) {
      padding-top: 2rem;
      padding-bottom: 2rem;
      padding-left: 0.5rem;
      padding-right: 0.5rem;
    }
    &::before {
      position: absolute;
      content: "";
      left: 0;
      top: 40%;
      width: 100%;
      height: 136px;
      background: linear-gradient(
        180deg,
        rgba(247, 247, 249, 0) 0%,
        #f7f7f9 100%
      );
      @media screen and (max-width: 899px) {
        top: 70%;
      }
    }
    &-menubar {
      display: flex;
      border-bottom: solid #ebebf3 0.5px;
      list-style: none;
      @media screen and (max-width: 531px) {
        width: 100%;
      }
      .menubar-options {
        margin-left: 2rem;
        color: #9896a1;
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 24px;
        @media screen and (max-width: 537px) {
          margin-left: 1rem;
          font-size: 13px;
        }
        &:first-child {
          color: #0a041c;
          font-weight: 500;
          border-bottom: solid #7445fb 4px;
          padding-bottom: 0.5rem;
        }
        &:hover {
          cursor: pointer;
          color: #0a041c;
        }
      }
    }
    .others-crypto {
      list-style: none;
      .crypto {
        background: #ffffff;
        border: 1px solid #ebebf3;
        border-radius: 8px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding-left: 1rem;
        padding-right: 1rem;
        padding-top: 1.5rem;
        padding-bottom: 1.5rem;
        margin-bottom: 1rem;
        margin-top: 1rem;
        &-circle {
          background: #ffffff;
          border: 1px solid #ebebf3;
          width: 48px;
          height: 48px;
          border-radius: 2rem;
          display: flex;
          align-items: center;
          justify-content: center;
          @media screen and (max-width: 704px) {
            width: 30px;
            height: 30px;
          }
          .crypto-logo {
            width: 24px;
            @media screen and (max-width: 704px) {
              width: 20px;
            }
          }
        }
        .btc-box {
          display: flex;
          flex-direction: column;
          @media screen and (max-width: 704px) {
            margin-left: 1rem;
          }
          .btc {
            text-transform: uppercase;
            color: #9896a1;
            font-weight: 400;
            font-size: 14px;
            line-height: 14px;
            margin-bottom: 0.5rem;
            @media screen and (max-width: 685px) {
              font-size: 11px;
            }
          }
          .crypto-name {
            color: #0a041c;
            font-weight: 600;
            font-size: 14px;
            line-height: 14px;
            @media screen and (max-width: 685px) {
              font-size: 11px;
            }
          }
        }
        .current-price-box {
          display: flex;
          flex-direction: column;
          text-align: center;
          width: 62px;
          @media screen and (max-width: 704px) {
            margin-left: 1rem;
          }
          .price {
            color: #9896a1;
            font-weight: 400;
            font-size: 14px;
            line-height: 14px;
            margin-bottom: 0.5rem;
            @media screen and (max-width: 685px) {
              font-size: 11px;
            }
          }
          .current-balance {
            color: #0a041c;
            font-weight: 600;
            font-size: 14px;
            line-height: 14px;
            @media screen and (max-width: 685px) {
              font-size: 11px;
            }
          }
        }
        .change-precent-box {
          display: flex;
          flex-direction: column;
          @media screen and (max-width: 704px) {
            margin-left: 1rem;
          }
          .change {
            color: #9896a1;
            font-weight: 400;
            font-size: 14px;
            line-height: 14px;
            margin-bottom: 0.5rem;
            @media screen and (max-width: 685px) {
              font-size: 11px;
            }
          }
          .change-precent-down {
            display: flex;
            align-items: center;
            color: #ea4d4d;
            font-weight: 600;
            font-size: 14px;
            line-height: 14px;
            @media screen and (max-width: 685px) {
              font-size: 11px;
            }
            img {
              margin-left: 0.5rem;
              @media screen and (max-width: 685px) {
                margin-left: 0.3rem;
                width: 13px;
              }
            }
          }
          .change-precent-up {
            display: flex;
            align-items: center;
            color: #2dc78f;
            font-weight: 600;
            font-size: 14px;
            line-height: 14px;
            img {
              margin-left: 0.5rem;
            }
          }
        }
        .line-up,
        .line-down {
          margin-left: 2rem;
          margin-right: 2rem;
        }
        .line-up,
        .line-down {
          @media screen and (max-width: 770px) {
            width: 100px;
          }
          @media screen and (max-width: 639px) {
            width: 50px;
            margin-left: 1rem;
            margin-right: 1rem;
          }
        }
      }
    }
  }
  .summary-box-mobile {
    margin-top: 5rem;
    align-self: center;
    background: #f7f7f9;
    border-radius: 16px;
    width: 509px;
    height: 400px;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    @media screen and (max-width: 899px) {
      width: 80%;
    }
    @media screen and (max-width: 600px) {
      width: 100%;
    }
    .title-box {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-left: 1rem;
      padding-right: 1rem;
      padding-top: 0.8rem;
      width: 100%;
      height: 3rem;
      img {
        width: 16px;
      }
    }
    #myChart2 {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      padding: 1.5rem;
      @media screen and (max-width: 1004px) {
        padding: 1rem;
      }
      @media screen and (max-width: 600px) {
        padding: 0.5rem;
      }
    }
  }
}
</style>
