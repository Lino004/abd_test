<template>
  <v-row
    align="center"
    justify="center"
    v-if="tabData.length"
  >
    <v-col>

      <!-- Bloc d'intercation global avec le test -->
      <v-container v-if="show === 0">

        <!-- Bloc titre et niveau -->
        <v-layout justify-center>
          <v-flex xs8>
            <v-container>
              <v-row>
                <v-col class="font-weight-bold title"> {{tabData[niveau].titre}} </v-col>
                <v-col class="text-end font-weight-bold title"> Niveau {{niveau + 1}}/{{tabData.length}}</v-col>
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
                <v-row justify="space-between" v-if="!tabData[niveau].demarre">
                  <v-col>
                    <v-card>
                      <v-responsive height="250">
                        <v-row align="center" style="height: 100%">
                          <v-col class="text-center">
                            <v-btn rounded large color="#2DC0EF" class="white--tex" @click="demarre">Cliquer ici pour demarrer le niveau {{niveau + 1}}</v-btn>
                          </v-col>
                        </v-row>
                      </v-responsive>
                    </v-card>
                  </v-col>
                </v-row>

                <!-- Bloc de visualisation du test -->
                <v-row justify="space-between" v-if="tabData[niveau].demarre">
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
        <v-layout justify-center v-if="tabData[niveau].demarre">
          <v-flex xs8 pa-5 class="text-center">
            <p class="display-1 font-weight-bold"> {{seconde}} s</p>
          </v-flex>
        </v-layout>
      </v-container>

      <!-- Composant resutat du test -->
      <Resultat :data="tabData" v-if="show === 1"/>

    </v-col>
  </v-row>
</template>

<script>
import Resultat from '@/components/Resultats.vue'

export default {
  name: 'test',
  components: { Resultat },
  data: () => ({
    tabData: [],
    niveau: 0,
    indiceMot: 0,
    seconde: 0,
    secondes: 0,
    show: 0,
  }),
  computed: {
    mot() {
      return this.tabData[this.niveau].aLire[this.indiceMot]
    }
  },
  watch: {
    indiceMot(val) {
      if (val >= this.tabData[this.niveau].aLire.length) {
        this.tabData[this.niveau].chrono = this.secondes
        this.stopTime()
        this.seconde = 0
        this.secondes = 0
        this.niveau += 1
        this.indiceMot = 0
      }
    },
    seconde(val) {
      if (val > 5) {
        this.note(0)
      }
    },
    niveau(val) {
      if (val >= this.tabData.length) {
        this.niveau = 0
        this.show = 1
      }
    }
  },
  methods: {
    note(val) {
      if (this.indiceMot < this.tabData[this.niveau].aLire.length) {
        this.tabData[this.niveau].score += val
      }
      this.indiceMot += 1
      this.seconde = 0
    },
    addS() {
      this.seconde += 1;
      this.secondes += 1;
    },
    initTime() {
      this.timer = setInterval(this.addS, 1000);
    },
    stopTime() {
      clearInterval(this.timer);
    },
    demarre() {
      this.tabData[this.niveau].demarre = true
      this.initTime()
    }
  },
  mounted() {
    this.tabData = [
      {
        titre: 'Graphèmes',
        aLire: ['a','o','i','u','e','é','è','y','p','t','c','f','s','b','g','d','v','z','j','l','r','m','k','n','h','q','ç'],
        demarre: false,
        score: 0,
        chrono: 0
      },
      {
        titre: 'Lecture de voyelles complexes',
        aLire: ['an','on','in','eu','ou','oi','au','ei','ai','oin','et','ion','ein','ien','ail','ain','eau','oeu','eil','ill','euil','ouil'],
        demarre: false,
        score: 0,
        chrono: 0
      },
      {
        titre: 'Lecture de syllabes simples',
        aLire: ['pa','te','co','fi','su','bi','ga','dé','vu','za','jo','li','re','mè','ko','né','ça'],
        demarre: false,
        score: 0,
        chrono: 0
      },
      {
        titre: 'Lecture de syllabes complexes',
        aLire: ['pla','tro','pri','col','dar','fur','gor','sal','alp','splo'],
        demarre: false,
        score: 0,
        chrono: 0
      },
      {
        titre: 'Lecture de mots réguliers',
        aLire: ['Papa','pomme','vélo','table','panier','fourmi','porte','guitare','pigeon','chemise','fenêtre','banane','papillon','coin','champignon'],
        demarre: false,
        score: 0,
        chrono: 0
      },
      {
        titre: 'Lecture de mots irréguliers',
        aLire: ['Femme','doigt','monsieur','loup','banc','paon','hier','sept','ville','seconde','parfum','chorale','plomb','écho','août'],
        demarre: false,
        score: 0,
        chrono: 0
      }
    ]
  }
}
</script>

<style>

</style>