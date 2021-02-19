<template>
  <div class="container">
    <Form @formData="setDataFromForm($event)" @giveawayOwnerData="giveawayOwner = $event"/>
    
    <Note />

    <GiveawayOwner :giveawayOwnerData="giveawayOwner" v-if="giveawayOwner"/>

    <Winners :winnersData="{data: formData.data, peopleSelectNumber: formData.peopleSelectNumber}" v-if="formData.data" />

  </div>
</template>

<script>
import Form from '@/components/Form'
import GiveawayOwner from '@/components/GiveawayOwner'
import Winners from '@/components/Winners'
import Note from '@/components/Note'

export default {
  data() {
    return {
      formData: {
        data: null,
        peopleSelectNumber: 1,
      },
      giveawayOwner: null,
    }
  },
  components: {
    Form,
    GiveawayOwner,
    Winners,
    Note,
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
