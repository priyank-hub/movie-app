<template>
    <v-container v-if="loading">
        <div class="text-xs-center">
            <!-- <v-progress-circular
                indeterminate
                :size="150"
                :width="8"
                color="green">
            </v-progress-circular> -->
            <v-row dense>
                <v-col cols="12" sm="4" v-for="i in [1, 2, 3, 4, 5, 6]"
                        :key="i">
                    <v-sheet
                        color="darken-2"
                        class="pa-3"
                    >
                        <v-skeleton-loader
                        class="mx-auto"
                        type="card"
                        ></v-skeleton-loader>
                    </v-sheet>
                </v-col>
            </v-row>
        </div>
    </v-container>
    <v-container v-else>
      <v-row dense>
        <v-col
          v-for="card in cards"
          :key="card.id"
          cols="12"
          sm="4"
        >
            <v-card>
                <v-img
                :src="card.src"
                class="white--text align-end"
                gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                height="200px"
                >
                <v-card-title v-text="card.title"></v-card-title>
                </v-img>

                <v-card-actions>
                <v-spacer></v-spacer>

                <v-btn icon>
                    <v-icon>mdi-heart</v-icon>
                </v-btn>

                <v-btn icon>
                    <v-icon>mdi-bookmark</v-icon>
                </v-btn>

                <v-btn icon>
                    <v-icon>mdi-share-variant</v-icon>
                </v-btn>
                </v-card-actions>
            </v-card>
        </v-col>
      </v-row>
    </v-container>
</template>

<script>
import axios from 'axios';
  export default {
    name: 'LatestMovie',

    data() {
        return {
            wholeResponse: null,
            loading: true,
            poster: null,

            cards: [
                {id: 1, title: 'Pre-fab homes', src: 'https://cdn.vuetifyjs.com/images/cards/house.jpg', flex: 12 },
                {id: 2, title: 'Favorite road trips', src: 'https://cdn.vuetifyjs.com/images/cards/road.jpg', flex: 12 },
                {id: 3, title: 'Best airlines', src: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg', flex: 12 },
            ],
        }
    },
    async mounted() {
        // https://imdb-api.com/API/Posters/k_1sdz3zba/tt0468569
        await axios
            .get('https://imdb-api.com/en/API/Top250Movies/k_1sdz3zba')
            .then(response => {
                this.wholeResponse = response.data.items
                this.loading = false

                this.wholeResponse.forEach(movie => {
                    let imgUrl = `https://imdb-api.com/API/Posters/k_1sdz3zba/${movie.id}`

                    axios.get(imgUrl)
                    .then(response => {
                        console.log('resp', response.data);
                        this.poster = response.data.posters[0].link;
                    })

                    this.cards.push({
                        id: movie.id,
                        title: movie.title,
                        src: this.poster,
                        flex: 12,
                    })
                    this.poster = null
                });
            })
            .catch(error => {
                console.log(error)
            }

            // k_1sdz3zba
        );
        // this.getImages();
    },
    methods: {
        getImages() {
            console.log("get Images");
            this.wholeResponse.forEach(movie => {
                let imgUrl = `https://imdb-api.com/API/Posters/k_1sdz3zba/${movie.id}`

                axios.get(imgUrl)
                .then(response => {
                    console.log('resp', response.data);
                    // this.poster = response.data.posters[0].link;
                })
            });
        }
    }
  }
</script>
<style scoped>
    .v-progress-circular {
        margin: 1rem
    }
</style>
