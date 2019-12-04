<template>
  <v-row
    align="center"
    justify="center"
  >
    <v-col>
      <v-container>
        <v-layout
          wrap
          justify-center
        >
          <v-flex xs8>
            <v-card class="pa-3" v-if="show === 0" raised>
              <v-container class="text-center">
                <p class="headline red--text font-weight-bold mb-0">Bienvenue !!!</p>
              </v-container>
              <v-container v-if="showText === 0">
                <p class="body-2 mb-0">
                  Expliquer à votre enfant qu’il devra lire des mots qui
                  s’afficheront à l’écran le mieux possible et le plus
                  rapidement possible.
                </p>
              </v-container>
              <v-container v-if="showText === 1">
                <p class="body-2 mb-0">
                  Préciser lui que certains mots sont “des mots inventé, qui
                  n’existent pas et qui ne veulent rien dire” et qu’il faudra
                  lire ce qui est écrit sans chercher à comprendre.
                </p>
              </v-container>
              <v-container v-if="showText === 2">
                <p class="body-2 mb-0">
                  Si l’enfant lit bien le mot, cliquer sur <v-btn rounded small color="#2DC0EF" class="white--text">Correcte</v-btn> <br>
                  S’il ne lit pas bien le mot, cliquer sur <v-btn rounded small color="#2DC0EF" class="white--text">Incorrecte</v-btn> <br>
                  S’il ne lit n’arrive pas à lire pendant le chrono de 5secondes, le mot changera tout seul.
                </p>
              </v-container>
              <v-container>
                <v-row align="center" justify-space-between>
                  <v-col>
                    <p class="caption mb-0">
                      Ceci est un test de lecture extrait du test de dépistage
                      de la dyslexie (Odedys2) en licence CC.
                    </p>
                  </v-col>
                  <v-col md="2" class="text-center">
                    <v-btn
                      rounded
                      small
                      color="red"
                      class="white--text"
                      @click="prevText()"
                      v-if="showText !== 0">Precedent</v-btn>
                  </v-col>
                  <v-col md="2" class="text-center">
                    <v-btn rounded small color="red" class="white--text" @click="nextText()">Suivant</v-btn>
                  </v-col>
                </v-row>
              </v-container>
            </v-card>
            <v-card class="pa-3 border" v-if="show === 1" raised>
              <v-container class="text-center">
                <p class="display-1 font-weight-bold">Votre enfant est prêt ?</p>
              </v-container>
              <v-container class="text-center">
                <v-btn
                  rounded
                  small
                  color="red"
                  class="white--text"
                  @click="$router.replace('/test')"
                  v-if="showText !== 0">Demarrer</v-btn>
              </v-container>
              <v-btn
                color="red" dark small
                absolute top left
                fab @click="show = 0"
              >
                <v-icon>mdi-arrow-left-circle</v-icon>
              </v-btn>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-col>
  </v-row>
</template>

<script>

export default {
  name: 'description',
  data: () => ({
    show: 0,
    showText: 0,
  }),
  methods: {
    nextText() {
      if (this.showText === 2) {
        this.show = 1;
        this.showText = 2;
        return '';
      }
      this.showText += 1;
      return '';
    },
    prevText() {
      if (this.showText === 0) {
        this.showText = 0;
        return '';
      }
      this.showText -= 1;
      return '';
    },
  }
}
</script>
