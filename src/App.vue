<template>
  <v-app id="app">
    <h1>NFT DEMO</h1>
    <br/>
    <br/>
    <v-container fluid class="px-0">
      <v-card
        class="mx-auto"
        elevation="20"
        max-width="800"
        max-height="600"
        color="#E0F7FA"
      >
        <v-card-title class="ma-3 text-center">Connect NFT Contract</v-card-title>
        <template>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
              md="10"
            >
              <v-input
                append-icon="mdi-close"
                prepend-icon="mdi-account-key-outline"
                @click:append="clean_mnemonic"
              >
                <v-text-field
                  v-model="mnemonic"
                  label="mnemonic"
                  placeholder="input mnemonic here"
                ></v-text-field>
              </v-input>
            </v-col>
          </v-row>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
              md="10"
            >
              <v-input
                append-icon="mdi-close"
                prepend-icon="mdi-wallet"
                @click:append="clean_address"
              >
                <v-text-field
                  v-model="address"
                  label="address"
                  placeholder="input address here"
                ></v-text-field>
              </v-input>
            </v-col>
          </v-row>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
              md="3"
            >
              <v-btn
                depressed
                color="primary"
                @click="connect"
              >
                Connect
              </v-btn>
            </v-col>
            <v-col
              cols="3"
              sm="6"
              md="3"
            >
              <v-btn
                depressed
                color="error"
                @click="disconnect"
              >
                Disconnect
              </v-btn>
            </v-col>
          </v-row>
          <br/>
          <br/>
        </template>
      </v-card>
    </v-container>
    <br/>
    <br/>
    <v-container>
      <v-card
        class="mx-auto"
        elevation="20"
        max-width="800"
        max-height="1000"
        color="#E0F7FA"
      >
        <v-card-title class="ma-3 text-center">Issue new NFT</v-card-title>
        <template>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
              md="10"
            >
              <v-input
                append-icon="mdi-close"
                prepend-icon="mdi-clipboard-file"
                @click:append="clean_tokenID"
              >
                <v-text-field
                  v-model="tokenID"
                  label="tokenID"
                  placeholder="input tokenID"
                ></v-text-field>
              </v-input>
            </v-col>
          </v-row>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
              md="10"
            >
              <v-input
                append-icon="mdi-close"
                prepend-icon="mdi-link"
                @click:append="clean_tokenURL"
              >
                <v-text-field
                  v-model="tokenURL"
                  label="URL"
                  placeholder="input URL"
                ></v-text-field>
              </v-input>
            </v-col>
          </v-row>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
              md="10"
            >
              <v-input
                append-icon="mdi-close"
                prepend-icon="mdi-currency-usd"
                @click:append="clean_paywall"
              >
                <v-text-field
                  v-model="paywall"
                  label="Paywall (wei)"
                  placeholder="input Paywall"
                ></v-text-field>
              </v-input>
            </v-col>
          </v-row>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
              md="10"
            >
              <v-input
                append-icon="mdi-close"
                prepend-icon="mdi-sack-percent"
                @click:append="clean_rate"
              >
                <v-text-field
                  v-model="taxRate"
                  label="Tax Rate (%)"
                  placeholder="input Tax Rate"
                ></v-text-field>
              </v-input>
            </v-col>
          </v-row>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
            >
              <v-btn
                depressed
                color="primary"
                @click="sendIssue"
              >
                ISSUE
              </v-btn>
            </v-col>
          </v-row>
          <br/>
          <br/>
          <v-row
            align="center"
            justify="space-around"
          >
            <h2>{{issueError}}</h2>
          </v-row>
          <br/>
          <br/>
        </template>
      </v-card>
    </v-container>
    <br/>
    <br/>
    <v-container>
      <v-card
        class="mx-auto"
        elevation="20"
        max-width="800"
        max-height="600"
        color="#E0F7FA"
      >
        <v-card-title class="ma-3 text-center">Buy NFT</v-card-title>
        <template>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
              md="10"
            >
              <v-input
                append-icon="mdi-close"
                prepend-icon="mdi-clipboard-file"
                @click:append="clean_bTokenID"
              >
                <v-text-field
                  v-model="bTokenID"
                  label="tokenID"
                  placeholder="input tokenID"
                ></v-text-field>
              </v-input>
            </v-col>
          </v-row>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
              md="10"
            >
              <v-input
                append-icon="mdi-close"
                prepend-icon="mdi-wallet"
                @click:append="clean_issuer"
              >
                <v-text-field
                  v-model="issuer"
                  label="Issuer"
                  placeholder="input Issuer"
                ></v-text-field>
              </v-input>
            </v-col>
          </v-row>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
              md="10"
            >
              <v-input
                append-icon="mdi-close"
                prepend-icon="mdi-currency-usd"
                @click:append="clean_money"
              >
                <v-text-field
                  v-model="money"
                  label="Money (wei)"
                  placeholder="input Money"
                ></v-text-field>
              </v-input>
            </v-col>
          </v-row>
          <v-row
            align="center"
            justify="space-around"
          >
            <v-col
              cols="3"
              sm="6"
            >
              <v-btn
                depressed
                color="primary"
                @click="sendBuy"
              >
                BUY
              </v-btn>
            </v-col>
          </v-row>
          <br/>
          <br/>
          <v-row
            align="center"
            justify="space-around"
          >
            <h2>{{buyError}}</h2>
          </v-row>
          <br/>
          <br/>
        </template>
      </v-card>
    </v-container>
    <br/>
    <br/>
    <v-container>
      <h3>Token Issued</h3>
      <v-data-table
        :headers="headers"
        :items="issues"
        :items-per-page="5"
        @click:row="handleClickIssue"
        class="elevation-1"
      ></v-data-table>
    </v-container>
    <br/>
    <br/>
    <v-container>
      <h3>Token Bought</h3>
      <v-data-table
        :headers="headers"
        :items="boughts"
        :items-per-page="5"
        @click:row="handleClickBought"
        class="elevation-1"
      ></v-data-table>
    </v-container>
  </v-app>
</template>

<script>

export default {
  mounted()  {
    this.initWs()
  },
  data () {
    return {
      wss: null,
      issueError: "",
      buyError: "",
      headers: [
        { text: 'eventName', value: 'eventName' },
        { text: 'txHash', value: 'txHash' },
        { text: 'value', value: 'custom' }
      ],
      issues: [],
      boughts: [],
      mnemonic: "supreme sea mango clump fence ready remind rebuild fence copy scan capital",
      address: "0x9AE09eD32B1b0d35e995Cd77fEb49B75021B9d39",
      tokenID: "",
      tokenURL: "",
      paywall: "",
      money: "100000000000000",
      taxRate: "0",
      bTokenID: "",
      issuer: "",
    }
  },
  methods: {
    initWs() {
      const wss = new WebSocket("ws://localhost:3000")
      wss.onmessage = (msg) => {
        const {topic, content} = JSON.parse(msg.data)
        if (topic == "issue_error") {
          this.issueError = content
        }
        else if (topic == "buy_error") {
          this.buyError = content
        }
        else if (topic == "issue_success") {
          this.issues.push(content)
        }
        else if (topic == "buy_success") {
          this.boughts.push(content)
        }
      }
      this.wss = wss
    },
    clean_address() {
      this.address = ""
    },
    clean_mnemonic() {
      this.mnemonic = ""
    },
    clean_paywall() {
      this.paywall = "0"
    },
    clean_rate() {
      this.taxRate = "0"
    },
    clean_tokenURL() {
      this.tokenURL = ""
    },
    clean_tokenID() {
      this.tokenID = ""
    },
    clean_bTokenID() {
      this.bTokenID = ""
    },
    clean_issuer() {
      this.issuer = ""
    },
    clean_money() {
      this.money = "0"
    },
    handleClickIssue(row) {
      console.log(row, this.issues[row].txHash)
    },
    handleClickBought(row) {
      console.log(row, this.boughts[row].txHash)
    },

    connect() {
      this.wss.send(JSON.stringify({
        topic: "connect",
        content: {
          mnemonic: this.mnemonic,
          address: this.address
        }
      }))
    },
    disconnect() {
      this.wss.send(JSON.stringify({
        topic: "disconnect",
        content: {}
      }))
    },
    sendIssue() {
      this.issueError = ""
      this.wss.send(JSON.stringify({
        topic: "issue",
        content: {
          tokenID: parseInt(this.tokenID),
          tokenURL: this.tokenURL,
          fee: this.paywall,
          rate: parseInt(this.taxRate)
        }
      }))
    },
    sendBuy() {
      this.buyError = ""
      this.wss.send(JSON.stringify({
        topic: "buy",
        content: {
          tokenID: parseInt(this.bTokenID),
          issuer: this.issuer,
          value: this.money
        }
      }))
    }
  }
}
</script>
<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  #input-usage .v-input__prepend-outer,
  #input-usage .v-input__append-outer,
  #input-usage .v-input__slot,
  #input-usage .v-messages {
    border: 1px dashed rgba(0,0,0, .4);
  }
</style>

