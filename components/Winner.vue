<template>
    <b-card class="mt-3 imageControlWinner">
        <div class="winnersProfile">
          <a :href="winner.snippet.topLevelComment.snippet.authorChannelUrl">
            <img :src="winner.snippet.topLevelComment.snippet.authorProfileImageUrl" :alt="winner.snippet.topLevelComment.snippet.authorDisplayName">
          </a>
          <div>
            <b-card-title>Kazanan Üyenin Youtube Kullanıcı Adı</b-card-title>
            <b-card-text class="text-right">
              {{winner.snippet.topLevelComment.snippet.authorDisplayName}}
            </b-card-text>
          </div>
        </div>
        <b-card-title>Videoya Yaptığı Yorum</b-card-title>
        <b-card-text>
        {{winner.snippet.topLevelComment.snippet.textOriginal}}
        </b-card-text>
      <div class="d-flex justify-content-center">
        <b-button variant="primary" @click="openUserLink">Kazanın Profiline Git</b-button>
      </div>
    </b-card>
</template>

<script>
export default {
  props: {
    winner: {
      type: Object,
      required: true,
    },
  },
  methods: {
    openUserLink() {
      const userLink = this.winner.snippet.topLevelComment.snippet.authorChannelUrl;
      window.open(userLink, "_blank");
    }
  },
}
</script>

<style scoped>
.imageControlWinner img{
  width: 100px;
  height: 100px;
}
.winnersProfile {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  margin-bottom: 10px;
}
.winnersProfile img{
  margin-right: 10px;
}
</style>