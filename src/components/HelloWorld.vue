<template>
  <div>
    <el-button @click="watchAddress">开始监听</el-button>
    <el-button @click="unwatchAddress">取消监听</el-button>
  </div>
</template>




<script>
import BlocknativeSdk from 'bnc-sdk'
import Web3 from 'web3'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    watchAddress () {
      const web3 = new Web3(window.ethereum)
      const options = {
        dappId: 'de5f01a4-d9b3-4f1d-8c75-1eb581af0b09',
        networkId: 1
        // un-comment if you would like to log all transaction events
        // transactionHandlers: [event => console.log(event.transaction)]
      }
      const blocknative = new BlocknativeSdk(options)
      const address = '0x7a250d5630B4cF539739dF2C5dAcb4c659F2488D'
      const { emitter, details } = blocknative.account(address)
      emitter.on('all', transaction => {
        console.log(JSON.stringify(transaction))
      })
    },
    unwatchAddress () {
      const web3 = new Web3(window.ethereum)
      const options = {
        dappId: 'de5f01a4-d9b3-4f1d-8c75-1eb581af0b09',
        networkId: 1
        // un-comment if you would like to log all transaction events
        // transactionHandlers: [event => console.log(event.transaction)]
      }
      const blocknative = new BlocknativeSdk(options)
      const address = '0x7a250d5630B4cF539739dF2C5dAcb4c659F2488D'
      blocknative.unsubscribe(address)
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
