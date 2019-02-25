<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,
      <br>check out the
      <a
        href="https://cli.vuejs.org"
        target="_blank"
        rel="noopener"
      >vue-cli documentation</a>.
    </p>
    <h3>Platzi music {{hola}}</h3>
    <select v-model="selectedCountry">
      <option v-for="country in countries" :value="country.value">{{country.name}}</option>
    </select>
    <spinner v-show="loading" />
    <ul>
      <artist v-bind:key="artist.mbid" v-for="artist in artists" v-bind:artist="artist"/>
      <div>
        <li v-bind:key="artist.mbid" v-for="artist in artists">{{artist.name}}</li>
      </div>
    </ul>
  </div>
</template>

<script>
import getArtists from "./../api";
import Artist from "./artist.vue";
import Spinner from "./spinner.vue";

export default {
  name: "HelloWorld",
  components: {
    Artist,
    Spinner
  },
  data() {
    return {
      hola: "hooooola",
      artists: [],
      countries: [
        { name: "Argentina", value: "argentina" },
        { name: "Colombia", value: "colombia" },
        { name: "España", value: "spain" }
      ],
      selectedCountry: "colombia",
      loading: true
    };
  },
  props: {
    msg: String
  },
  methods: {
    refreshArtist: function() {
      const self = this;
      this.loading = true;
      getArtists(this.selectedCountry).then(function(artists) {
        self.artists = artists;
        self.loading = false
      });
    }
  },
  mounted: function() {
    this.refreshArtist()
  },
  watch: {
    selectedCountry: function () {
      this.refreshArtist();
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
