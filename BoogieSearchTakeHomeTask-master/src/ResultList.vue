<template>
  <div
    class="flex flex-col items-center bg-white rounded-lg border shadow-md md:flex-row md:max-w-xl hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700 pb-1 text-left mb-1 ml-4"
  >
    <img
      class="object-cover w-full h-96 rounded-t-lg md:h-auto md:w-48 md:rounded-none md:rounded-l-lg"
      :src="getFanArtUrl"
      width="250"
      height="250"
    />

    <div class="flex flex-col justify-between p-4 leading-normal">
      <h5
        class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white text-blue-700"
      >
        {{ year }}
      </h5>
      <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
        {{ albumName }}
      </p>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    year: Number,
    albumName: String,
    artistFanArtList: Array,
  },
  created() {
    console.log("artistFanArtListIn==>", this.artistFanArtList);
  },
  computed: {
    getFanArtUrl() {
      const urlIndex = this.randomIntFromInterval();
      console.log(urlIndex, this.artistFanArtList[urlIndex]);
      const artistFanArtUrl = this.artistFanArtList[urlIndex];
      console.log("artistFanArtUrl", artistFanArtUrl);
      return artistFanArtUrl;
    },
  },
  methods: {
    randomIntFromInterval(min = 0, max = 3) {
      // min and max included
      return Math.floor(Math.random() * (max - min + 1) + min);
    },
  },
};
</script>
<style>
highlightColor {
  padding-top: 10%;
  color: purple;
  font-family: "arial";
  font-weight: bolder;
  font-size: 1rem;
}
highlightColor {
  padding-top: 50%;
  font-family: "arial";
  font-weight: bolder;
  font-size: 1rem;
}
</style>
