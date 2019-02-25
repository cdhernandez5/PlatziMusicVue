<template>
  <li class="artist">
      <h2>
          <a :href="artist.url">{{artist.name}}</a>
      </h2>
      <img :src="artist.image[2]['#text']"/>
  </li>
</template>

<script>
export default {
  name: 'artist',
  props: [ 'artist' ]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
li.artist
    display block
    margin  10px 0
</style>
