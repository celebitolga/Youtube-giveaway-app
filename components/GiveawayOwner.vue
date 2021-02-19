<template>
  <b-card :img-src="giveawayOwnerData.snippet.thumbnails.high.url" :img-alt="giveawayOwnerData.snippet.localized.title" img-right class="mt-3 imageControl">
      <b-card-title>Video Başlığı</b-card-title>
      <b-card-text>
        {{giveawayOwnerData.snippet.localized.title}}
      </b-card-text>
      <b-card-title>Video Açıklaması</b-card-title>
      <b-card-text>
      {{giveawayOwnerData.snippet.localized.description}}
      </b-card-text>
    <div class="d-flex justify-content-center">
      <b-button variant="primary" @click="openVideoLink">Videoya git</b-button>
    </div>
  </b-card>
</template>

<script>
export default {
  props: {
    giveawayOwnerData: {
      type: Object,
      required: true,
    },
  },
  methods: {
    openVideoLink() {
      const videoLink = "https://www.youtube.com/watch?v=" + this.giveawayOwnerData.id;
      window.open(videoLink, "_blank");
    },
  },
}
</script>

<style>
.imageControl .card-body{
  overflow-x: hidden;
  overflow-y: auto;
}
.imageControl img {
  width: 50%;
  height: 100%;
}
@media (max-width: 992px) { 
  .imageControl {
    flex-direction: column !important;
  }
  .imageControl img{
    width: auto;
    height: 300px;
  }
}
</style>