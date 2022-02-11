<template>
  <div class="">
    <div class="py-2 relative">
      <button @click="$emit('click', dataApi)">
        <img
          :src="`http://image.tmdb.org/t/p/w500/${dataApi.poster_path}`"
          alt=""
          style="width: 250px"
          class="px-2 rounded-xl"
        />
        <p class="text-center py-2 font-semibold">
          {{ dataApi.title }} ({{ date(dataApi.release_date) }})
        </p>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    dataApi: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
    date(value) {
      var date = new Date(value);
      var getYear = date.getFullYear();
      return getYear;
    },
  },
};
</script>

<style>
.div-vote{
  border: black 1px solid;
  background-color: rgb(8, 8, 8);
}
</style>
