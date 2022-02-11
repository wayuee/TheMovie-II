<template>
  <div class="div-body">
    <label class="pl-10 font-semibold text-xl">The Movie</label>
    <input
      type="text"
      class="ml-10 border rounded-xl px-7 py-2 mt-3"
      v-model="search"
      placeholder="Search Name"
    />
    <div class="grid grid-cols-5 ml-1 pt-5">
      <DataApi
        v-for="(data, id) in dataFilmSearch"
        :key="id"
        :data-api="data"
        @click="detailPage(data)"
      />
    </div>
    <div class="flex justify-center">
      <button
        @click="moreAdd"
        class="py-2 px-10 border font-semibold rounded-xl text-black hover:bg-black hover:text-white"
      >
        More
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import DataApi from "~/components/DataApi";
export default {
  components: {
    axios,
    DataApi,
  },
  data() {
    return {
      dataFilm: [],
      search: "",
      page: 1,
    };
  },
  mounted() {
    this.getDataFromApi();
  },
  methods: {
    getDataFromApi() {
      var api =
        "https://api.themoviedb.org/3/movie/now_playing?api_key=a4b5770b8ab225dfad78f779a8f3262c&language=en-US&page=" +
        this.page +
        "";
      axios
        .get(api)
        .then((res) => {
          this.dataFilm = res.data.results;
          console.log(this.dataFilm);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    detailPage(value) {
      this.$router.push(`/_detail?id=${value.id}`);
    },
    moreAdd() {
      this.page += 1;
      this.getDataFromApi();
    },
  },
  computed: {
    dataFilmSearch() {
      return this.dataFilm.filter((data) => {
        return data.title.toLowerCase().match(this.search);
      });
    },
  },
};
</script>

<style>
.div-body {
  background: linear-gradient(rgba(51, 50, 50, 0.5), rgba(92, 90, 90, 0.5));
}
</style>
