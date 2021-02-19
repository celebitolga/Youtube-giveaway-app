<template>
  <div class="container">
    <Form @formData="data = $event"/>
    
    <div v-if="data != null">
      {{data}}
    </div>


    <b-card class="mt-3" v-if="userInput != null">
      <pre class="m-0">{{ userInput }}</pre>
    </b-card>

    
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
      data: null,
    }
  },
  components: {
    Form,
    GiveawayOwner,
    Winners,
  },
};
</script>

<style>
</style>
