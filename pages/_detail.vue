<template>
  <div class="div-body pt-5 pl-3 h-screen">
    <nuxt-link to="/" class="nuxt-link rounded-xl px-5 py-2 font-semibold"
      >Back</nuxt-link
    >
    <div class="flex justify-center relative">
      <h2 class="div-title text-3xl font-semibold">{{ dataDetail.title }}</h2>
    </div>
    <div class="mt-5 ml-10 mr-48">
      <img
        :src="`http://image.tmdb.org/t/p/w500/${dataDetail.poster_path}`"
        class="float-left mr-5 rounded-xl"
        alt=""
        style="width: 320px"
      />
      <p class="span-overview relative text-justify mb-2">
        <span class="font-semibold text-lg">Overview :</span>
        {{ dataDetail.overview }}
      </p>
      <hr class="mb-3" />
      <span class="font-semibold"
        >Genre :
        <span
          v-for="(data, id) in dataDetail.genres"
          :key="id"
          class="font-normal inline-block"
        >
          {{ `${data.name} ,` }}</span
        >-</span
      >
      <span class="font-semibold float-right"
        >RunTime :
        <span class="font-normal mr-20">{{ dataDetail.runtime }}M</span></span
      ><br />
      <span class="font-semibold"
        >Tagline :
        <span class="font-normal">{{ dataDetail.tagline }}</span></span
      ><span class="float-right font-semibold mr-28"
        >Rate :
        <span v-if="dataDetail.vote_average <= 5" class="text-red-700">{{
          dataDetail.vote_average
        }}</span
        ><span
          v-else-if="dataDetail.vote_average >= 6"
          class="text-green-800"
          >{{ dataDetail.vote_average }}</span
        ></span
      >
      <p class="font-semibold text-lg mb-4">
        Company Production :
        <span
          class="font-normal"
          v-for="(data, id) in dataDetail.production_companies"
          :key="id"
          >{{ `${data.name} ,` }}</span
        >-
      </p>
      <h3 class="font-bold text-xl">Stars:</h3>
      <span
        class="font-semibold inline-block"
        v-for="(data, id) in dataStars.slice(0, 10)"
        :key="id"
        >{{ `${data.name} ,` }}</span
      >-
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  components: {
    axios,
  },
  data() {
    return {
      id: this.$route.query.id,
      dataDetail: [],
      dataStars: [],
    };
  },
  mounted() {
    this.getApiName();
    this.getApiStars();
  },
  methods: {
    getApiName() {
      var api =
        "https://api.themoviedb.org/3/movie/" +
        this.id +
        "?api_key=6de3c0f0176c22fabe34c6be66fa8cae";
      axios
        .get(api)
        .then((res) => {
          this.dataDetail = res.data;
          console.log(this.dataDetail);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    getApiStars() {
      var api_2 =
        "https://api.themoviedb.org/3/movie/" +
        this.id +
        "/credits?api_key=6de3c0f0176c22fabe34c6be66fa8cae";
      axios
        .get(api_2)
        .then((res) => {
          this.dataStars = res.data.cast;
          console.log(this.dataStars);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
.div-body {
  background: linear-gradient(rgba(39, 38, 38, 0.5), rgba(65, 60, 60, 0.5));
}
.nuxt-link {
  background-color: rgba(47, 49, 11, 0.452);
  color: rgb(55, 241, 179);
}
.div-title::after {
  content: "";
  height: 2px;
  width: 20%;
  background: #141414;
  position: absolute;
  left: calc(50% - 10%);
  bottom: -5px;
}
</style>
