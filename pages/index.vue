<template>
  <div class="page-about">
    <h1 class="page-background-text">NFT TILES</h1>
    <div class="content">
      <div class="header">
        <img src="~/assets/logo.png" alt="" />
        <a href="/">Home</a>
        <a href="/home">How it works</a>
        <a href="/home">FAQ</a>
        <a href="/home">Contacts</a>
      </div>
      <div>
        <button @click="initWeb3()" class="save-buttons__save">
          {{ text }}
        </button>
      </div>
      <div class="main">
        <h1 class="title">
          <span>10</span> UNIQUE <br />
          NFT TILES
        </h1>
        <p class="title-description">
          Participate in the auction for each tile.
        </p>
        <p class="title-description">
          The buyer gets the opportunity to leave a message.
        </p>
        <p class="title-description title-description-unique">
          The tiles can be resold.
        </p>
      </div>
      <div class="blocks">
        <div class="none"></div>

        <nuxt-link
          v-for="item in tokens"
          :to="`/nft/${item}`"
          :key="item"
          class="block"
        >
          <div>
            <img
              src="https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg"
              alt=""
              class="img-size"
            />
            <p class="block-price">0.1</p>
            <p class="block-price-dollar">$416</p>
          </div>
          <div class="buy-now-link">Buy now!</div>
        </nuxt-link>

        <div class="none"></div>
      </div>
    </div>
    <div class="footer">
      <p>© 2021 10 Tiles LTD.</p>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      text: 'Wallet',
      connected: 0,
      tokens: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
      images: [],
      image:
        'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
    }
  },
  mounted() {
    this.reqURIs()
    this.checkConnection()
  },
  methods: {
    async initWeb3() {
      try {
        // Ask to connect
        await window.ethereum.send('eth_requestAccounts')
      } catch (error) {
        // User denied account access
        console.error('User denied web3 access', error)
        return
      }
    },
    // checkConnection() {
    //   console.log(this.$accounts)
    //   if (this.$accounts.length === 0) {
    //     this.text = 'Connect Wallet'
    //   } else {
    //     this.text = 'Connected'
    //   }
    // },
    async reqURIs() {
      try {
        this.tokens.forEach((token) => {
          let val = this.$contract.methods.tokenURI(token).call()
          console.log(val)
          this.images.append(val)
        })
      } catch (error) {
        console.log('error getting uri for images')
        console.log(error)
        this.images = [
          'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
          'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
          'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
          'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
          'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
          'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
          'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
          'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
          'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
          'https://zgiizmhvja6iuvd4rufqcnu2ld4xcpfk7xdafyfqdavt4efa3e4a.arweave.net/yZCMsPVIPIpUfI0LATaaWPlxPKr9xgLgsBgrPhCg2Tg',
        ]
      }
    },
  },
}
</script>
<style lang='scss'>
.page-about {
  min-height: 100vh;
  height: 100%;
  background: rgb(9, 9, 126);
  background: linear-gradient(38deg, #09097e 24%, #510074 100%);
  position: relative;
  display: grid;
  grid-template-rows: 1fr auto;
  padding: 0 16px;

  .page-background-text {
    position: absolute;
    top: 262px;
    left: 0;
    right: 0;
    font-size: 320px;
    white-space: nowrap;
    font-family: 'Bungee', cursive;
    color: rgba(255, 255, 255, 0.2);
    overflow: hidden;
  }
  .content {
    max-width: 1200px;
    width: 100%;
    margin: 0 auto;

    background-image: url('~/assets/man.png');
    background-repeat: no-repeat;
    background-position: right 50px;
    background-size: 600px;

    .main {
      .title {
        font-size: 75px;
        line-height: 66px;
        color: #00fc7b;
        font-weight: 400;
        font-family: 'Bungee', cursive;
        margin-top: 200px;
        margin-bottom: 40px;
        span {
          color: #00ffff;
        }
      }
      .title-description {
        margin-bottom: 16px;
        font-size: 16px;
        line-height: 24px;
        //color: #ffffff;
        font-weight: 600;
      }
      .title-description-unique {
        margin-top: 30px;
        color: #00fc7b;
      }
      margin-bottom: 240px;
    }
    .blocks {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr 1fr;
      gap: 24px;
      padding-bottom: 100px;

      .block {
        padding: 20px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        border: 2px dashed rgba(255, 255, 255, 0.5);
        min-height: 282px;
        border-radius: 30px;
        transition: 0.3s;
        .img-size {
          width: 100px;
          height: 100px;
        }
        .buy-now-link {
          background: #090069;
          padding: 18px;
          border-radius: 12px;
          text-align: center;
        }
        .block-price {
          color: #00fc7b;
          line-height: 1.5;
          display: flex;
          align-items: center;
          font-size: 24px;
          &:after {
            content: url('~/assets/eth.png');
            margin-left: 4px;
          }
        }
        .block-price-dollar {
          font-size: 14px;
        }
        &:hover {
          cursor: pointer;
          -webkit-box-shadow: 1px 14px 62px 11px rgba(0, 252, 123, 1);
          -moz-box-shadow: 1px 14px 62px 11px rgba(0, 252, 123, 1);
          box-shadow: 1px 14px 62px 11px rgba(0, 252, 123, 1);
          background: white;
          transition: 0.3s;
        }
      }
    }
  }
  @media screen and (max-width: 768px) {
    background: linear-gradient(38deg, #09097e 80%, #af00ff 100%);
    .page-background-text {
      display: none;
    }
    .content {
      background-size: 300px;
      background-position: right 100px;
      .header {
        a {
          font-size: 14px;
        }
      }
      .main {
        margin-bottom: 50px;
        .title {
          font-size: 60px;
        }
      }
      .blocks {
        grid-template-columns: 1fr 1fr;
        .none {
          display: none;
        }
        .block {
          min-height: 180px;
        }
      }
    }
  }
}
</style>
