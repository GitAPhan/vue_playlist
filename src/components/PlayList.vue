<template>
  <div id="playlist_container">
    <h1>Playlist</h1>
  </div>
</template>

<script>
export default {
  name: "play-list",
  methods: {
    // this function to to display song on PageSong when track is clicked
    view_song(payload) {
      // this function and the same function in SongList should be the same but returns different values.
      var view_selected_track = this.songs[payload.currentTarget.id - 1];
      this.$root.$emit("view_track", view_selected_track);

      // going to try global emit to SongList and use the view_song function there.
      // this.$root.$emit('playlist_view_track', payload);
      // that didnt work, abort mission
    },
    add_song_function(payload) {
      //   grabbing container where song will be added
      var playlist_container = document.getElementById("playlist_container");
      // song container where all the song information will be appended to
      var song_container = document.createElement("article");
      // visual styling done to container
      song_container.style.display = "grid";
      song_container.style.placeItems = "center";
      song_container.style.backgroundColor = "skyblue";
      song_container.style.borderRadius = "15px";
      song_container.style.border = "black solid 1px";
      song_container.style.height = "200px";
      song_container.style.width = "100%";
  // gave container id for easy reference and added click event listener to display track info in PageSong area
      song_container.id = payload;
      song_container.addEventListener('click', this.view_song);

      // grabbing the song according to the id = tracklist
      var song_to_be_added = this.songs[payload - 1];
      //   creating h2 element to contain song title
      var song_title = document.createElement("h2");
      song_title.innerText = song_to_be_added.song_name;
      //   creating h3 element to contain song artist name
      var song_artist = document.createElement("h3");
      song_artist.innerText = song_to_be_added.song_artist;
      //   creating h4 element to contain duration of song
      var song_duration = document.createElement("h4");
      // converting the time to m:ss format
      var minutes = Math.floor(song_to_be_added.song_duration / 60);
      var seconds = song_to_be_added.song_duration - minutes * 60;
      song_duration.innerText = minutes + ":" + seconds;
    //   creating remove button 
    var remove_button = document.createElement('button');
    remove_button.innerText = "-";
    remove_button.style.width = "90%";
    remove_button.style.borderRadius = "15px";
    remove_button.style.fontSize = "25px";
    remove_button.addEventListener('click', this.remove_song_function);

      // let the appending begin
      song_container.appendChild(song_title);
      song_container.appendChild(song_artist);
      song_container.appendChild(song_duration);
      song_container.appendChild(remove_button);

      playlist_container.appendChild(song_container);
    },
    // function to remove selected song from playlist
    remove_song_function(card){
          var emit_data = card.target.parentElement.id;
        //   global emit id for reference to add back song to playlist
          this.$root.$emit('removeSong', emit_data);
        //   turn current card display to none
          card.target.parentElement.remove();
    }
  },
  mounted() {
    // global emit from SongList for when the user clicks add song
    this.$root.$on("addSong", this.add_song_function);
  },
  data() {
    return {
      songs: [
        // realizing now that having multiple sources of the same data can couse discrepancies 
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

div {
  width: 100%;
  overflow-y: scroll;
  font-size: 0.8rem;
  row-gap: 10px;
  padding: 45px 15px 0px;
  grid-area: b;
  display: grid;
  overflow-y: scroll;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-template-rows: 202px 202px;
  column-gap: 10px;
  row-gap: 10px;
  justify-items: start;
  align-items: center;
}

h1 {
  position: absolute;
  top: 20px;
  right: calc((100% - 430px)/2 - 42px);
  background-color: white;
}
</style>