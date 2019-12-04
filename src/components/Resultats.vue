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
            ></v-data-table>
          </v-container>
          <v-container>
            <p class="headline font-weight-bold text-center">Score tatal du test : {{score}} </p>
            <p class="headline red--text font-weight-bold text-center"> {{message}} </p>
            <div>
              <v-btn rounded small color="red" class="white--text">Retourner à l'acceuil</v-btn>
            </div>
          </v-container>
        </v-card>
      </v-flex>
    </v-layout>

  </v-container>
</template>

<script>
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
    message() {
      if (this.score <= 86) return 'Votre enfant a un pourcentage jugé à risque de la dyslexie'
      return 'Votre enfant n’est pas à risque'
    }
  }
}
</script>

<style>

</style>