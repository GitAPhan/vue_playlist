<template>
  <div>
    <h1>YTV Big Fun Party Mix 9</h1>
    <!-- v-for loop to put playlist on page -->
    <!-- click function to show clicked card in PageSong area -->
    <article
      @click="view_song"
      v-for="song in songs"
      :id="song.tracklist"
      :key="song.tracklist"
    >
    <!-- track light info below -->
      <h2>Track Name: {{ song.song_name }}</h2>
      <h3>Artist: {{ song.song_artist }}</h3>
      <h4>{{ timeCalculation(song.song_duration) }}</h4>
      <!-- add click event to button. Add clicked card to playlist -->
      <button @click="add_to_playlist">+</button>
    </article>
  </div>
</template>

<script>
export default {
  name: "song-list",
  methods: {
    // this function to to display song on PageSong when track is clicked
    view_song(payload) {
      // [payload-1] = index 
      var view_selected_track = this.songs[payload.currentTarget.id - 1];
      this.$root.$emit("view_track", view_selected_track);
    },
    //   this function is to convert the song duration from seconds to m:ss
    timeCalculation(time) {
      var minutes = Math.floor(time / 60);
      var seconds = time - minutes * 60;
      var timeConvert = minutes + ":" + seconds;
      return timeConvert;
    },
    //   this function is to remove card and emit card id to playlist to add song
    // wasn't sure if this was the method you wanted us to go in
    // just in case I sent objects with the PageSong component 
    add_to_playlist(card) {
      //   turn current card display to none by toggle hidden_card class
      card.path[1].classList.toggle("hidden_card");
      var emit_data = card.target.parentElement.id;
      //   global emit id to playlist
      this.$root.$emit("addSong", emit_data);
    },
    readd_removed_song(payload) {
      // grabbed all hidden_card element
      var removed_songs = document.getElementsByClassName("hidden_card");
      // loop to go through array
      for (var i = 0; i < removed_songs.length; i++) {
        // conditional to toggle hidden_card class if payload matches id
        if (removed_songs[i].id == payload);
        removed_songs[i].classList.toggle("hidden_card");
        return;
      }
    },
  },
  mounted() {
    // global emit from PlayList for when the user click remove song from playlist
    this.$root.$on("removeSong", this.readd_removed_song);

    // payload from PlayList view_song function to use view_song function on this page
    this.$root.$on("playlist_view_card", this.view_song_two);
  },
  data() {
    return {
      songs: [
        // I kind of cheated and put all the song data on the 3 pages. I wouldn't do it like this
        // in the future, because IF i had to hard code data next time, I would use vuex
        {
          song_name: "The Sweet Escape",
          song_artist: "Gwen Stefani",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Aliaune "Akon" Thiam, Giorgio Tuinfort, Gwen Stefani`,
          song_duration: 221,
          tracklist: 1,
        },
        {
          song_name: "Stronger",
          song_artist: "Kanye West",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Kanye West
Written-By ["Harder, Better, Faster, Stronger" Sample] – Edwin Birdsong, Guy Manuel De Homen-Christo*, Thomas Bangalter`,
          song_duration: 272,
          tracklist: 2,
        },
        {
          song_name: "Hey There Delilah",
          song_artist: "Plain White T's",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Tom Higgenson`,
          song_duration: 218,
          tracklist: 3,
        },
        {
          song_name: "One More Chance",
          song_artist: "will-i-am",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Fernando Garibay, W. (will-i-am) Adams`,
          song_duration: 254,
          tracklist: 4,
        },
        {
          song_name: "Because Of You",
          song_artist: "Ne-Yo",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – M. Eriksen*, S. Smith*, T. Hermansen*`,
          song_duration: 235,
          tracklist: 5,
        },
        {
          song_name: "He Said She Said",
          song_artist: "Ashley Tisdale",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Evan "Kidd" Bogart*, Jonathan Rotem*, Ryan "Alias" Tedder*`,
          song_duration: 182,
          tracklist: 6,
        },
        {
          song_name: "Ladies' Choice",
          song_artist: "Zac Efron",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Marc Shaiman, Scott Wittman`,
          song_duration: 141,
          tracklist: 7,
        },
        {
          song_name: "With Love",
          song_artist: "Hilary Duff",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Hilary Duff, Julius Diaz, Kara DioGuardi, Vada Nobles`,
          song_duration: 168,
          tracklist: 8,
        },
        {
          song_name: "Grace Kelly",
          song_artist: "MIKA",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Dan Warner, Jodi Marr, John Merchant, MIKA (8)`,
          song_duration: 176,
          tracklist: 9,
        },
        {
          song_name: "Say It Right (Remix)",
          song_artist: "Nelly Furtado",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Producer – Danja, Timbaland
Remix [Mixed By] – Dummies*
Written-By – Nate Hills, Nelly Furtado, Tim Mosley*`,
          song_duration: 407,
          tracklist: 10,
        },
        {
          song_name: "DJ Play My Song",
          song_artist: "Jully Black",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Johnny "Natural" Najara*, Jully Black, Keith Harris`,
          song_duration: 310,
          tracklist: 11,
        },
        {
          song_name: "It Makes Me Happy",
          song_artist: "Drake Bell",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – C.J. Abraham, Drake Bell, Michael Corcoran`,
          song_duration: 128,
          tracklist: 12,
        },
        {
          song_name: "She's So Sorry",
          song_artist: "Hedley",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Brian Howes, Chris Crippin, Dave Rosin, Jacob Hoggard, Tom MacDonald (4)`,
          song_duration: 206,
          tracklist: 13,
        },
        {
          song_name: "Stuck For The Summer",
          song_artist: "Two Hours Traffic",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Two Hours Traffic`,
          song_duration: 218,
          tracklist: 14,
        },
        {
          song_name: "Clumsy",
          song_artist: "Fergie",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Bobby Troup, Stacy Ferguson, Will Adams`,
          song_duration: 228,
          tracklist: 15,
        },
        {
          song_name: "Crush On You",
          song_artist: "Nuclear Donkey",
          song_album: "YTV Big Fun Party Mix 9",
          song_info: `Written-By – Bobby Troup, Stacy Ferguson, Will Adams`,
          song_duration: 239,
          tracklist: 16,
        },
      ],
    };
  },
};
</script>

<style scoped>
* {
  margin: 0px;
  padding: 0px;
}

article {
  display: grid;
  place-items: center;
  background-color: skyblue;
  border-radius: 15px;
  width: 100%;
  height: 150px;
  align-self: start;
}

.hidden_card {
  display: none;
  pointer-events: none;
}

button {
  font-size: 20px;
  text-align: center;
  width: 90%;
  border-radius: 15px;
}

div {
  width: 400px;
  height: 90vh;
  overflow-y: scroll;
  font-size: 0.8rem;
  display: grid;
  place-items: center;
  grid-template-rows: 50px 150px 150px 150px 150px 150px 150px 150px 150px;
  row-gap: 10px;
  padding: 0px 15px;
  grid-area: a;
}

h1 {
  position: sticky;
  top: 0px;
  background-color: white;
  padding: 10px;
  width: 100%;
}
</style>