<template>
  <div>
    <!-- conditional: show this if all the displayed song variables are undefined -->
    <h1
      v-if="
        this.displayed_song_three == undefined &&
        this.displayed_song_two == undefined &&
        this.displayed_song == undefined
      "
    >
      Click on a track to view more
    </h1>
    <!-- Displayed title elsewise -->
    <h1 v-else>Track Info</h1>
    <!-- display this article only when displayed_song is defined -->
    <article v-if="displayed_song != undefined">
      <h2>
        Track {{ displayed_song.tracklist }}:{{ displayed_song.song_name }}
      </h2>
      <h3>Artist: {{ displayed_song.song_artist }}</h3>
      <h4>Album: {{ displayed_song.song_album }}</h4>
      <h5>Time: {{ displayed_song.song_duration }}s</h5>
      <p>{{ displayed_song.song_info }}</p>
    </article>
    <!-- display this article only when displayed_song_two is defined -->
    <article v-if="displayed_song_two != undefined">
      <h2>
        Track {{ displayed_song_two.tracklist }}:{{
          displayed_song_two.song_name
        }}
      </h2>
      <h3>Artist: {{ displayed_song_two.song_artist }}</h3>
      <h4>Album: {{ displayed_song_two.song_album }}</h4>
      <h5>Time: {{ displayed_song_two.song_duration }}s</h5>
      <p>{{ displayed_song_two.song_info }}</p>
    </article>
    <!-- display this article only when displayed_song_three is defined -->
    <article v-if="displayed_song_three != undefined">
      <h2>
        Track {{ displayed_song_three.tracklist }}:{{
          displayed_song_three.song_name
        }}
      </h2>
      <h3>Artist: {{ displayed_song_three.song_artist }}</h3>
      <h4>Album: {{ displayed_song_three.song_album }}</h4>
      <h5>Time: {{ displayed_song_three.song_duration }}s</h5>
      <p>{{ displayed_song_three.song_info }}</p>
    </article>
  </div>
</template>

<script>
export default {
  name: "page-song",
  data() {
    return {
      displayed_song: undefined,
      displayed_song_two: undefined,
      displayed_song_three: undefined,
      // variable to determine which of the displayed_song will be updated when display_track function is called
      display_order: 1,
    };
  },
  methods: {
    display_track(payload) {
      // tried to write code to only allow a track to be displayed once.
      // Doesn't work well when clicking the track from the playlist and songlist
      // conditional: to run only if payload doesn't match whats already displayed
      if (
        this.displayed_song_three != payload &&
        this.displayed_song_two != payload &&
        this.displayed_song != payload
      ) {
        // conditional: to determine which display song variable to update according to variable display_order
        if (this.display_order === 1) {
          this.displayed_song = payload;
          // increase value of display_order
          this.display_order++;
        } else if (this.display_order === 2) {
          this.displayed_song_two = payload;
          this.display_order++;
        } else {
          this.displayed_song_three = payload;
          // change display_order value back to 1
          this.display_order = 1;
        }
      }
    },
  },
  mounted() {
    this.$root.$on("view_track", this.display_track);
  },
};
</script>

<style scoped>
* {
  margin: 0px;
  padding: 0px;
}

div {
  grid-area: c;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 50px 1fr;
  justify-items: center;
  align-items: end;
  overflow: hidden;
  width: 100%;
  height: 300px;
  align-self: end;
}
article {
  overflow: hidden;
  padding: 10px;
}

h1 {
  grid-column: span 3;
  justify-self: center;
}

</style>