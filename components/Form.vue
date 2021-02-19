<template>
  <div>
    <Loading v-if="loading"/>

    <b-form @submit.prevent="onSubmit" @reset.prevent="onReset" v-if="show" class="mt-3">
      <b-form-group label="Youtube video Linki" label-for="videoLink">
        <b-form-input
          id="videoLink"
          v-model="userInput.videoLink"
          type="text"
          placeholder="Video linki"
          required
        ></b-form-input>
      </b-form-group>
    
      <b-form-group
        label="Seçilecek yorum kelimesi (İsteğe bağlı) Örneğin; Çekilişe katıldım, katıldım vs."
        label-for="usercomment"
      >
        <b-form-input
          id="usercomment"
          type="text"
          v-model="userInput.comment"
          placeholder="Seçilecek yorum kelimesi (İsteğe bağlı)"
        ></b-form-input>
      </b-form-group>
    
      <b-form-group
        label="Kaç kişi seçilecek (1-100)"
        label-for="userPeopleSelectNumber"
      >
        <b-form-input
          id="userPeopleSelectNumber"
          type="number"
          min="1"
          max="100"
          v-model="userInput.peopleSelectNumber"
          placeholder="Seçilecek kişi sayısı"
          required
        ></b-form-input>
      </b-form-group>
    
      <div class="text-center">
        <b-button type="submit" variant="primary">Çekiliş Yap</b-button>
        <b-button type="reset" variant="danger">Formu Yenile</b-button>
      </div>
    </b-form>
  </div>
</template>

<script>
import Loading from '@/components/Loading'

export default {
  components: {
    Loading,
  },
  data() {
    return {
      userInput: {
        videoLink: "",
        comment: "",
        peopleSelectNumber: 1,
      },
      show: true,
      loading: false,
    };
  },
  methods: {
    async onSubmit() {
      //Loading screen
      this.loading = true;
      //
      let url;

      const videoId = await this.getVideoId(this.userInput.videoLink);
      if(!videoId) {
        return false;
      }

      const giveawayOwner = await this.$axios.get(`https://youtube.googleapis.com/youtube/v3/videos?part=snippet&contentDetails&statistics&id=${ videoId }&key=${ $nuxt.context.env.apiKey }`)
            .then(response => response.data.items[0]);
      
      if(this.userInput.comment.trim().length > 0) {
        // For utf-8, there is comment
        const comment = encodeURIComponent(this.userInput.comment.trim())
        url = `https://youtube.googleapis.com/youtube/v3/commentThreads?part=snippet&searchTerms=${ comment }&videoId=${ videoId }&key=${ $nuxt.context.env.apiKey }&maxResults=100`;
      } else {
        // no comment
        url = `https://youtube.googleapis.com/youtube/v3/commentThreads?part=snippet&videoId=${ videoId }&key=${ $nuxt.context.env.apiKey }&maxResults=100`;
      }

      //Get peoples who did comment to video
      const data = await this.$axios.get(url)
            .then(response => response.data.items);

      // emit data, giveawayOwner
      this.$emit("formData", { giveawayOwner, data, peopleSelectNumber: this.userInput.peopleSelectNumber });

      //loading screen
      this.loading = false;
    },
    onReset() {
      this.userInput = {
        videoLink: "",
        comment: "",
        peopleSelectNumber: 1,
      };
    },
    getVideoId(videoLink) {
      let videoId;
      if (videoLink.includes("https://www.youtube.com/watch?v=")) {
        videoId = videoLink.split("https://www.youtube.com/watch?v=")[1];
      } else if (videoLink.includes("www.youtube.com/watch?v=")) {
        videoId = videoLink.split("www.youtube.com/watch?v=")[1];
      } else if (videoLink.includes("youtube.com/watch?v=")) {
        videoId = videoLink.split("youtube.com/watch?v=")[1];
      } else if (videoLink.includes("https://youtu.be/")) {
        videoId = videoLink.split("https://youtu.be/")[1];
      } else if (videoLink.includes("youtu.be/")) {
        videoId = videoLink.split("youtu.be/")[1];
      } else {
        return false;
      }
      return videoId;
    },
  },

};
</script>

<style>
</style>