<template>
    <v-container v-if="loading">
        <div class="text-xs-center">
        <v-progress-circular
            indeterminate
            :size="150"
            :width="8"
            color="green">
        </v-progress-circular>
        </div>
    </v-container>
    <!-- <v-container v-else grid-list-lg>
        <v-layout wrap>
        <v-flex xs4
            v-for="(item, index) in wholeResponse"
            :key="index"
            mb-2>
            <v-card>
                <v-img
                    :src="item.Poster"
                    aspect-ratio="1"
                ></v-img>
                <v-card-title primary-title>
                    <div>
                        <h2>{{item.Title}}</h2>
                        <div>Year: {{item.Year}}</div>
                        <div>Type: {{item.Type}}</div>
                        <div>IMDB-id: {{item.imdbID}}</div>
                    </div>
                </v-card-title>
                <v-card-actions class="justify-center">
                    <v-btn text
                    color="green"
                    @click="singleMovie(item.imdbID)"
                    >View</v-btn>
                </v-card-actions>
            </v-card>
        </v-flex>
        </v-layout>
    </v-container> -->
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

            cards: [
                {id: 1, title: 'Pre-fab homes', src: 'https://cdn.vuetifyjs.com/images/cards/house.jpg', flex: 12 },
                {id: 2, title: 'Favorite road trips', src: 'https://cdn.vuetifyjs.com/images/cards/road.jpg', flex: 12 },
                {id: 3, title: 'Best airlines', src: 'https://cdn.vuetifyjs.com/images/cards/plane.jpg', flex: 12 },
            ],
        }
    },
    mounted() {
        axios
            .get('https://imdb-api.com/en/API/Search/k_1sdz3zba/kuch')
            .then(response => {
                this.wholeResponse = response.data.results
                this.loading = false
                // console.log('response', this.wholeResponse);

                this.wholeResponse.forEach(movie => {
                    this.cards.push({
                        id: movie.id,
                        title: movie.title,
                        src: movie.image,
                        flex: 12,
                    })
                });
            })
            .catch(error => {
                console.log(error)
            }
            // k_1sdz3zba
        );
    }
  }
</script>
<style scoped>
    .v-progress-circular {
        margin: 1rem
    }
</style>
