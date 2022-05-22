<template>
  <div class="w-full h-full relative ">
    <img
      id="headerBannerimg"
      class="w-full h-full mix-blend-lighten opacity-20 "
      :src="headerArtUrl"
    />
    <h1 class=" uppercase text-center">{{ greetingMessage }}</h1>
    <h1 class=" absolute bottom-0 left-0 uppercase">{{ greetingMessageName }}</h1>
  </div>
</template>
<script>
//w-96 h-44
//w-96 h-44 float-right
export default {
  props: {
    greetingMessage: String,
    greetingMessageName: String,
    headerArtUrl: String,
  },
  data() {
    return {};
  },
  computed: {
    compStyle() {
      return {
        "background-image": `url('${this.headerArtUrl}')`,
        "background-blend-mode": "lighten",
        opacity: "0.20",
      };
    },
  },
};

// text-align: left;
//     margin: 2rem;
</script>
<style>
h1 {
  padding-top: 5rem;
  color: white;
  font-family: "arial";
  font-weight: bolder;
  font-size: 3rem;
}
</style>
