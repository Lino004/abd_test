<template>
  <v-row
    align="center"
    justify="center"
    v-if="tabData.length"
  >
    <v-col>

      <!-- Bloc d'intercation global avec le test -->
      <v-container>

        <!-- Bloc titre et niveau -->
        <v-layout justify-center>
          <v-flex xs8>
            <v-container>
              <v-row>
                <v-col> {{tabData[niveau].titre}} </v-col>
                <v-col class="text-end">  {{niveau + 1}}/{{tabData.length}}</v-col>
              </v-row>
            </v-container>
          </v-flex>
        </v-layout>

        <!-- Bloc d'intereaction avec le test -->
        <v-layout
          wrap
          justify-center
        >
          <v-flex xs8>
            <v-card raised>
              <v-container>

                <!-- Bloc de demarrage du test -->
                <v-row justify="space-between">
                  <v-col>
                    <v-card>
                      <v-responsive height="250">
                        <v-row align="center" style="height: 100%">
                          <v-col class="text-center">
                            <v-btn rounded color="#2DC0EF" class="white--text" @click="correcte()">Cliquer ici pour demarrer</v-btn>
                          </v-col>
                        </v-row>
                      </v-responsive>
                    </v-card>
                  </v-col>
                </v-row>

                <!-- Bloc de visualisation du test -->
                <v-row justify="space-between">
                  <v-col>
                    <v-card>
                      <v-responsive height="250">
                        <v-row align="center" style="height: 100%">
                          <v-col class="text-center">
                            <p class="display-3 font-weight-bold"> {{mot}} </p>
                          </v-col>
                        </v-row>
                      </v-responsive>
                    </v-card>
                  </v-col>
                  <v-col md="4">
                    <v-row align="end" justify="end" style="height: 100%">
                      <v-col class="text-center">
                        <div class="mb-2">
                          <v-btn rounded small color="#2DC0EF" class="white--text" @click="note(1)">Correcte</v-btn>
                        </div>
                        <div>
                          <v-btn rounded small color="#2DC0EF" class="white--text" @click="note(0)">Incorrecte</v-btn>
                        </div>
                      </v-col>
                    </v-row>
                  </v-col>
                </v-row>

              </v-container>
            </v-card>
          </v-flex>
        </v-layout>

        <!-- Bloc du chrono -->
        <v-layout justify-center>
          <v-flex xs8 pa-5 class="text-center">
            <p class="display-1 font-weight-bold">5s</p>
          </v-flex>
        </v-layout>
      </v-container>

      <!-- Composant resutat du test -->
      <Resultat/>
      
    </v-col>
  </v-row>
</template>

<script>
import jsonData from '@/config/data'
import Resultat from '@/components/Resultats.vue'

export default {
  components: { Resultat },
  data: () => ({
    tabData: [],
    niveau: 0,
    indiceMot: 0,
  }),
  computed: {
    mot() {
      return this.tabData[this.niveau].aLire[this.indiceMot]
    }
  },
  watch: {
    indiceMot(val) {
      if (val > this.tabData[this.niveau].aLire.length) {
        this.niveau += 1
        this.indiceMot = 0
      }
    }
  },
  methods: {
    note(val) {
      this.tabData[this.niveau].score += val
      this.indiceMot += 1
    },
  },
  mounted() {
    this.tabData = jsonData
  }
}
</script>

<style>

</style>