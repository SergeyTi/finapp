<template lang="pug">
.content
  .module
    .module-in
      h1.title
        .name(:class="`account${account.id}`")  {{ account.name }}
        .name {{ account.currency }}
        .sup {{ account.id }}

  .module._bg
    .module-in
      TrnsList(:trns="trnsList")
</template>


<script>
import { mapGetters } from 'vuex'
import TrnsList from './TrnsList.vue'

export default {

  computed: {
    ...mapGetters(['trns']),

    account() {
      return this.$store.state.accounts.all.find(a => a.id === +this.$route.params.id)
    },

    trnsList() {
      return this.trns
        .filter(trn => trn.accountId === this.account.id)
        .slice(0, 30)
    }
  },

  components: { TrnsList }
}
</script>
