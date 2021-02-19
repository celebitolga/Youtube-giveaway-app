<template>
  <div class="container">
    <Form @formData="setDataFromForm($event)"/>

    <GiveawayOwner :giveawayOwnerData="formData.giveawayOwner" v-if="formData.giveawayOwner"/>

    <Winners :winnersData="formData.data" v-if="formData.data" />

  </div>
</template>

<script>
import Form from '@/components/Form'
import GiveawayOwner from '@/components/GiveawayOwner'
import Winners from '@/components/Winners'

export default {
  data() {
    return {
      userInput: null,
      formData: {
        giveawayOwner: null,
        data: null,
      },
    }
  },
  components: {
    Form,
    GiveawayOwner,
    Winners,
  },
  methods: {
    setDataFromForm(data) {
      this.formData = {...data};
    },
  },
};
</script>

<style>
</style>
