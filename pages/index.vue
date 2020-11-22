  
<template>
  <v-row class="pl-2">
    <!-- A fazer -->
    <v-col cols="6" sm="3">
      <v-card elevation="2" class="px-4 py-2 pb-3">
        <h4 class="pb-1">A fazer</h4>
        <listcards :data="cards"> </listcards>
        <!-- botao adiconar -->
        <v-btn
          v-if="addCardAF"
          text
          style="display: flex; flex: 1"
          class="btn-card px-2"
          @click="openCard('AF')"
        >
          <v-icon
            size="20"
            class="d-inline grey--text"
            style="vertical-align: top"
          >
            mdi-plus-thick
          </v-icon>
          <h4 class="grey--text ml-1">Adicionar tarefa</h4>
        </v-btn>
        <inserircartao
          v-on:textcard="addCartao($event, 'cards')"
          v-on:closeCard="openCard('AF')"
          v-on:update="key++"
          v-else
        >
        </inserircartao>
      </v-card>
    </v-col>
    <!-- \A fazer -->
    <!-- Em andamento -->
    <v-col cols="6" sm="3">
      <v-card elevation="2" class="px-4 py-2 pb-3">
        <h4 class="pb-1">Em andamento</h4>
        <listcards :data="cardsEA"> </listcards>
        <!-- botao adiconar -->
        <v-btn
          v-if="addCardEA"
          text
          style="display: flex; flex: 1"
          class="btn-card px-2"
          @click="openCard('EA')"
        >
          <v-icon
            size="20"
            class="d-inline grey--text"
            style="vertical-align: top"
          >
            mdi-plus-thick
          </v-icon>
          <h4 class="grey--text ml-1">Adicionar tarefa</h4>
        </v-btn>

        <inserircartao
          v-on:textcard="addCartao($event, 'cardsEA')"
          v-on:update="key++"
          v-on:closeCard="openCard('EA')"
          v-else
        >
        </inserircartao>
      </v-card>
    </v-col>
    <!-- \Em andamento -->
    <!-- Concluido  -->
    <v-col cols="6" sm="3">
      <v-card elevation="2" class="px-4 py-2 pb-3">
        <h4 class="pb-1">Concluido</h4>
        <listcards :data="cardsC"> </listcards>
        <!-- botao adiconar -->
        <v-btn
          v-if="addCardC"
          text
          style="display: flex; flex: 1"
          class="btn-card px-2"
          @click="openCard('C')"
        >
          <v-icon
            size="20"
            class="d-inline grey--text"
            style="vertical-align: top"
          >
            mdi-plus-thick
          </v-icon>
          <h4 class="grey--text ml-1">Adicionar tarefa</h4>
        </v-btn>
        <inserircartao
          v-on:textcard="addCartao($event, 'cardsC')"
          v-on:closeCard="openCard('C')"
          v-on:update="key++"
          v-else
        >
        </inserircartao>
      </v-card>
    </v-col>
    <!-- \Concluido  -->
  </v-row>
</template>

<script lang="ts">
import {
  Component,
  Inject,
  Model,
  Prop,
  Provide,
  Vue,
  Watch,
} from 'nuxt-property-decorator'

import inserircartao from '../components/inserircartao.vue'
import listcards from '../components/listcards.vue'

@Component({
  components: { inserircartao, listcards },
  //components: { Logo },
})
export default class MyComponent extends Vue {
  key: number = 0
  // variavel responsavel por abrir textarea para add cartao
  addCardAF: boolean = true
  addCardEA: boolean = true
  addCardC: boolean = true
  // Abre textarea para add cartao
  openCard(state: any) {
    if (state == 'AF') {
      this.addCardAF = !this.addCardAF
    } else if (state == 'EA') {
      this.addCardEA = !this.addCardEA
    } else if (state == 'C') {
      this.addCardC = !this.addCardC
    }
  }
  //dados da listagem <componente listarcards>
  cards: any[] = [] // recebe valor em array do local storage
  cardsEA: any[] = []
  cardsC: any[] = []

  getcards() {
    this.cards = JSON.parse(localStorage.getItem('cards') as any)
  }
  getcardsEA() {
    this.cardsEA = JSON.parse(localStorage.getItem('cardsEA') as any)
  }
  getcardsC() {
    this.cardsC = JSON.parse(localStorage.getItem('cardsC') as any)
  }

  mounted() {
    this.getcards()
    this.getcardsEA()
    this.getcardsC()
  }

  cardLocalstorage: any[] = [] //recebe dados do local storage convertido em array
  saveLocalstorage: string = '' //variavel devolvida ao localstorage co o novo valor

  addCartao(ValueText: string | any, type: string) {
    console.log(type)
    if (type == 'cards') {
      this.cardLocalstorage = ValueText
      this.cards.push(this.cardLocalstorage)
      this.saveLocalstorage = JSON.stringify(this.cards)
    } else if (type == 'cardsEA') {
      this.cardLocalstorage = ValueText
      this.cardsEA.push(this.cardLocalstorage)
      this.saveLocalstorage = JSON.stringify(this.cardsEA)
    } else if (type == 'cardsC') {
      this.cardLocalstorage = ValueText
      this.cardsC.push(this.cardLocalstorage)
      this.saveLocalstorage = JSON.stringify(this.cardsC)
    }

    localStorage.setItem(type, this.saveLocalstorage)
  }
}
</script>

<style>
button.btn-card:hover {
  background-color: #e5e5e5;
  transition: 0.3s;
}



.col-6 {
    padding: 2px;
    margin-left: 0.6rem;
}

</style>