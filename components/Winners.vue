<template>
   <div class="mt-3">
    <Loading v-if="loading"/>
    <div class="text-center">
      <h1 v-if="winnersData.peopleSelectNumber == 1"><b-badge variant="success">Kazanan</b-badge></h1>
      <h1 v-else><b-badge variant="success">Kazananlar</b-badge></h1>
    </div>

    <Winner  v-for="(winner, index) in winners" :winner="winner" :key="'winner-' + index"/>
    
    <NoCommitError v-if="winners.length == 0" />
  </div>
</template>

<script>
import Winner from '@/components/Winner'
import NoCommitError from '@/components/NoCommitError'
import Loading from '@/components/Loading'

export default {
  components: {
    Winner,
    NoCommitError,
    Loading,
  },
  data() {
    return {
      loading: false,
    }
  },
  props: {
    winnersData: {
      type: Object,
      required: true,
    },
  },
  computed: {
    winners() {
      return this.choseWinners();
    }
  },
  methods: {
    choseWinners() {
      this.loading = true;

      const dataLength = this.winnersData.data.length;
      const winnersPeople = [];
      const loop = this.winnersData.peopleSelectNumber > dataLength ? dataLength : this.winnersData.peopleSelectNumber;
      for(let i = 0; i < loop; i++) {
        winnersPeople.push(this.winnersData.data[this.getRandomInt(dataLength)]);
      }
      
      this.loading = false;
      return winnersPeople;
    },
    getRandomInt(max) {
      return Math.floor(Math.random() * Math.floor(max));
    }
  },
}
</script>

<style>

</style>