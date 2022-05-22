<template>
  <div class="searchresult">
    <div class="flex flex-col">
      <div class="bg-gradient-to-b from-violet-900 to-cyan-900">
        <PageHeader
          :greetingMessageName="this.$route.query.q"
          :headerArtUrl="artistLogo"
        />
      </div>
      <div class="flex">
        <div class="w-1/2">
          <p class="font-semibold m-4 text-left">
            Found
            <span class="text-blue-700">{{ artists.length }} </span> results for
            <span class="text-blue-700 uppercase">"{{ this.$route.query.q }}"</span>
          </p>
          <ul class="albumList">
            <li v-for="(value, index) in artists" :key="index" class="pb-1">
              <!-- <b>Album:</b>{{value.strAlbum}} <b>Relased:</b>{{value.intYearReleased}} -->
              <!--<ResultList :year="value.intYearReleased" :albumName="value.strAlbum" :artistLogo="value.strArtistLogo"/> -->
              <ResultList
                :year="value.intYearReleased"
                :albumName="value.strAlbum"
                :artistFanArtList="artistFanArtList"
              />
            </li>

            <!-- <li>
            <h2>Artist Details</h2>
          </li> -->
            <!-- <li v-for="(value, index) in artistDetail" :key="index">
            <b>ArtistID:</b> {{ value.idArtist }} <b>Biography:</b
            >{{ value.strBiographyEN }}
          </li> -->
          </ul>
        </div>
        <div class="w-1/2 place-items-center h-screen">
          <h5 class="m-4 font-bold">Artist Gallery</h5>
          <div class="m-4 self-center w-1/2" style="margin: auto;">
            <div
              v-for="(value, index) in artistFanArtList"
              :key="index"
              class="max-w-sm rounded overflow-hidden shadow-lg text-center pb-1"
            >
              <img class="w-full" :src="value" alt="Sunset in the mountains" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import PageHeader from "../PageHeader.vue";
import ResultList from "../ResultList.vue";

export default {
  data() {
    return {
      artists: "",
      artistDetail: "",
      artistFanArtList: [],
      artistLogo: "",
    };
  },

  components: {
    PageHeader,
    ResultList,
  },
  created() {
    console.log();
    this.getAtristInformation();
    this.getAllAlbumdetails();
  },
  methods: {
    async getAllAlbumdetails() {
      await axios
        .get(
          `https://theaudiodb.com/api/v1/json/2/discography.php?s=` +
            this.$route.query.q
        )
        .then((response) => {
          console.log("===>123", response.data);
          this.artists = response.data.album;
        });
    },
    async getAtristInformation() {
      await axios
        .get(
          `https://theaudiodb.com/api/v1/json/2/search.php?s=` +
            this.$route.query.q
        )
        .then((response) => {
          // console.log("===>123567", response.data);
          // console.log("===>6666666 this.artistFanArt", this.artistFanArtList);
          this.artistFanArtList.push(response.data.artists[0].strArtistFanart);
          this.artistFanArtList.push(response.data.artists[0].strArtistFanart2);
          this.artistFanArtList.push(response.data.artists[0].strArtistFanart3);
          this.artistFanArtList.push(response.data.artists[0].strArtistFanart4);
          this.artistLogo = response.data.artists[0].strArtistBanner;
          this.artistDetail = response.data.artists;
          console.log("===>123 this.artists", response.data.artists[0]);
          console.log(
            "===>1235678899 this.artistFanArt",
            this.artistFanArtList
          );
        });
    },
  },
};
</script>
<style scoped>
.heading {
  height: 10rem;

  width: max-width;
  align-content: center;
}
h1 {
  padding-top: 5rem;
  color: white;
  font-family: "arial";
  font-weight: bolder;
  font-size: 3rem;
  text-align: left;
}
li {
  border-block-start-color: black;
  border-block-style: solid;
}
</style>
