<template>
  <v-container>

    <!-- Bloc d'intereaction avec le test -->
    <v-layout
      wrap
      justify-center
    >
      <v-flex xs8>
        <v-card raised>
          <v-card-title>Resultats du test</v-card-title>
          <v-container>
            <v-data-table
              :headers="headers"
              :items="data"
              class="elevation-1"
              hide-default-footer
            >
              <template v-slot:item.score="{ item }">
                <v-chip :color="getColor(item)" dark>{{ item.score }}</v-chip>
              </template>
              <template v-slot:item.chrono="{ item }">
                <strong dark>{{ item.chrono }} s</strong>
              </template>
            </v-data-table>
          </v-container>
          <v-container>
            <p class="headline font-weight-bold text-center">Score tatal du test : {{score}} </p>
            <p class="headline font-weight-bold text-center">Temps total : {{time}} </p>
            <p class="headline font-weight-bold text-center" :class="score <= 86 ? 'red--text' : 'green--text'"> {{message}} </p>
            <v-row justify="space-between">
              <v-col md="4">
                <v-btn rounded color="amber" @click="$router.push('/')">Retourner à l'acceuil</v-btn>
              </v-col>
              <v-col md="4" class="text-end">
                <v-btn
                  rounded
                  color="amber"
                  href="http://abc.futurix.tech/la-dyslexie/">
                  En savoir plus
                </v-btn>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-flex>
    </v-layout>

  </v-container>
</template>

<script>
import moment from 'moment'

moment().locale('fr')

export default {
  props: [ 'data' ],
  data: () => ({
    headers: [
      { text: 'Titre', value: 'titre' },
      { text: 'Score', value: 'score' },
      { text: 'Temps', value: 'chrono' },
    ],
  }),
  computed: {
    score() {
      let score = 0
      this.data.map(el => el.score).forEach(el => {
        score += el
      });
      return score
    },
    time() {
      let time = 0
      this.data.map(el => el.chrono).forEach(el => {
        time += el
      });
      return moment(time, 's').format('H[h] m[mn] s[ss]')
    },
    message() {
      if (this.score <= 86) return 'Votre enfant a un pourcentage jugé à risque de la dyslexie'
      return 'Votre enfant n’est pas à risque'
    },
  },
  methods: {
    getColor (score) {
      if (score.titre === 'Graphèmes') return score.score <= 20 ? 'red' : 'green'
      if (score.titre === 'Lecture de voyelles complexes') return score.score <= 15 ? 'red' : 'green'
      if (score.titre === 'Lecture de syllabes simples') return score.score <= 14 ? 'red' : 'green'
      if (score.titre === 'Lecture de syllabes complexes') return score.score <= 7 ? 'red' : 'green'
      if (score.titre === 'Lecture de mots réguliers') return score.score <= 11 ? 'red' : 'green'
      if (score.titre === 'Lecture de mots irréguliers') return score.score <= 8 ? 'red' : 'green'
      return ''
    },
  }
}
</script>

<style>

</style>