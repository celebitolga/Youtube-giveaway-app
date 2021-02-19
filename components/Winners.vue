<template>
   <b-card class="mt-3">
    <pre class="m-0"> {{winnersData}} </pre>
  </b-card>
</template>

<script>
export default {
  props: {
    winnersData: {
      type: Array,
      required: true,
    },
  },
}
</script>

<style>

</style>