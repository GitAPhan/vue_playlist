<template>
  <div id="page_body">
    <play-list></play-list>
    <song-list></song-list>
    <page-song></page-song>
  </div>
</template>

<script>
import PlayList from "./PlayList.vue";
import SongList from "./SongList.vue";
import PageSong from "./PageSong.vue";

export default {
  name: "page-body",
  components: {
    PlayList,
    SongList,
    PageSong,
  },
};
</script>

<style scoped>
#page_body {
    display: grid;
    grid-auto-flow: column;
}
</style>