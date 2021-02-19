<template>
  <div class="container">
    <Form @formData="setDataFromForm($event)" @giveawayOwnerData="setGiveawayOwnerData($event)"/>
    
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
    setGiveawayOwnerData(data) {
      if(data == null) {
        this.giveawayOwner = null;
        this.formData = {
          data: null,
          peopleSelectNumber: 1,
        }
      } else {
        this.giveawayOwner = data;
      }
    },
  },
};
</script>

<style>
</style>
