<template>
  <div class="addressInput">
    <zk-input
      v-model="inputtedWallet"
      class="walletAddress"
      placeholder="0x address or Unstoppable Domain name"
      type="text"
    />

    <div class="errorTextContainer" v-show="address">
      <transition name="fadeFast">
        <div class="errorText text-xs text-green text-left">{{ address }}</div>
      </transition>
    </div>
    <div class="errorTextContainer">
      <transition name="fadeFast">
        <div v-if="error" class="errorText text-xs text-red text-left">{{ error }}</div>
      </transition>
    </div>
  </div>
</template>

<script lang="ts">
import Vue, { PropOptions } from "vue";
import { DecimalBalance } from "@matterlabs/zksync-nuxt-core/types";
import axios from "axios";
import { checkAddress } from "@/plugins/utils";

export default Vue.extend({
  props: {
    value: {
      type: String,
      default: "",
      required: false,
    } as PropOptions<DecimalBalance>,
  },
  data() {
    return {
      inputtedWallet: this.value ?? "",
      address: "",
    };
  },
  computed: {
    isValid(): boolean {
      return checkAddress(this.inputtedWallet);
    },
    error(): string {
      if (this.inputtedWallet && !this.isValid) {
        if (
          !this.inputtedWallet.startsWith("0x") &&
          !this.inputtedWallet.includes(".crypto") &&
          !this.inputtedWallet.includes(".zil") &&
          !this.inputtedWallet.includes(".nft") &&
          !this.inputtedWallet.includes(".blockchain") &&
          !this.inputtedWallet.includes(".bitcoin") &&
          !this.inputtedWallet.includes(".coin") &&
          !this.inputtedWallet.includes(".wallet") &&
          !this.inputtedWallet.includes(".888") &&
          !this.inputtedWallet.includes(".dao") &&
          !this.inputtedWallet.includes(".x")
        ) {
          return "Address should start with '0x' or unstoppable domain";
        }
        return "";
      } else {
        return "";
      }
    },
  },
  watch: {
    async inputtedWallet(val) {
      this.address = "";
      let unstopapa="";
      const trimmed = val.trim();
      if (
        trimmed.includes(".crypto") ||
        trimmed.includes(".zil") ||
        trimmed.includes(".nft") ||
        trimmed.includes(".blockchain") ||
        trimmed.includes(".bitcoin") ||
        trimmed.includes(".coin") ||
        trimmed.includes(".wallet") ||
        trimmed.includes(".888") ||
        trimmed.includes(".dao") ||
        trimmed.includes(".x")
      ) {
        const data = await axios.get("https://functions-drab.vercel.app/api/domain/" + trimmed);
        this.address = data.data.records["crypto.ETH.address"];
        unstopapa=trimmed;
      }
      this.$emit("haha",  {address:this.address!==""?this.address:val,unstoppableAddress:unstopapa});
      this.inputtedWallet = trimmed;

    },
    value(val) {
      this.inputtedWallet = val.address;
    },
  },
});
</script>
