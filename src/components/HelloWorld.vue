<template>
  <v-container align="center" justify="center" class="mx-auto">
    <v-row align="center" justify="center">
      <v-col cols="8">
        <v-card shaped elevation="30" outlined width="400" height="400">
          <v-card-title>
            <div>
              <h1 class="text-center" align="center" justify="center">
                My Music
              </h1>
            </div>
          </v-card-title>
          <v-divider></v-divider>
          <v-card-text>
            <div>
              <h2>
                {{ current.title }}- <span>{{ current.artist }}</span>
              </h2>
            </div>

            <div>
              <v-btn class="ma-2" color="indigo" dark @click="next">
                <v-icon dark>
                  mdi-skip-next
                </v-icon>
              </v-btn>
              <v-btn
                class="ma-2"
                color="indigo"
                dark
                v-if="!isPlaying"
                @click="play"
              >
                <v-icon dark>
                  mdi-play-circle
                </v-icon>
              </v-btn>
              <v-btn class="ma-2" color="indigo" dark v-else @click="pause">
                <v-icon dark>
                  mdi-pause
                </v-icon>
              </v-btn>
              <v-btn class="ma-2" color="indigo" dark @click="prev">
                <v-icon dark>
                  mdi-skip-previous
                </v-icon>
              </v-btn>
            </div>
            <div>
              <h3>The PlayList</h3>
              <v-btn
                depressed
                v-for="song in songs"
                :key="song.title"
                @click="play(song)"
              >
                {{ song.title }}-{{ song.artist }}
              </v-btn>

              <v-spacer></v-spacer>
            </div>
            <!-- {{songs[0].src}} -->
          </v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <div>
              <v-rating
                v-model="rating"
                color="yellow darken-3"
                background-color="grey darken-1"
                empty-icon="$ratingFull"
                half-increments
                hover
                large
              ></v-rating>
            </div>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    rating: 4.5,
    current: {
      // title: 'Song Title'
    },
    index: 0,
    isPlaying: false,
    songs: [
      {
        title: "Here I Am",
        artist: "Chris Tomil",
        src: require("../assets/Here_i_am-Chris_Tomil.mp3"),
      },
      {
        title: "On my way",
        artist: "Allan Walker",
        src: require("../assets/On my way-Allan Walker.mp3"),
      },
    ],
    player: new Audio(),
  }),

  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;

        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.currect = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.currect = this.songs[this.index];
      this.play(this.current);
    },
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  },
};
</script>

<style></style>
