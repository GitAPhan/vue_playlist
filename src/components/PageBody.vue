<template>
  <div id="page_body">
    <song-list></song-list>
    <page-song></page-song>
    <play-list></play-list>
  </div>
</template>
// nothing to special here to report
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
* {
  margin: 0px;
  padding: 0px;
}

#page_body {
    display: grid;
    grid-template-columns: 430px 1fr;
    grid-template-rows: 1fr 300px;
    width: 95%;
    height: 95vh;
    grid-template-areas: 
    "a b"
    "a c";
}
</style>