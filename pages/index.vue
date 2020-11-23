<template>
  <v-row class="pl-2">
    <!-- A fazer -->
    <v-col cols="6" sm="2">
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
          <h4 class="grey--text ml-1">Adicionar um cartao</h4>
        </v-btn>
        <inserircartao
          v-on:closeCard="openCard('AF')"
          v-on:textcard="addCartao($event, 'cards')"
          v-else
        >
        </inserircartao>
      </v-card>
    </v-col>
    <!-- \A fazer -->
    <!-- Em andamento -->
    <v-col cols="6" sm="2">
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
          <h4 class="grey--text ml-1">Adicionar um cartao</h4>
        </v-btn>

        <inserircartao
          v-on:closeCard="openCard('EA')"
          v-else
          v-on:textcard="addCartao($event, 'emAndamento')"
        >
        </inserircartao>
      </v-card>
    </v-col>
    <!-- \Em andamento -->
    <!-- Concluido  -->
    <v-col cols="6" sm="2">
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
          <h4 class="grey--text ml-1">Adicionar um cartao</h4>
        </v-btn>
        <inserircartao
          v-on:closeCard="openCard('C')"
          v-else
          v-on:textcard="addCartao($event, 'concluido')"
        >
        </inserircartao>
      </v-card>
    </v-col>
    <!-- \Concluido-->
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
  cards: any[] = [] //recebe dados do local storage convertido em array
  cardsEA: any[] = []
  cardsC: any[] = []

  getcards(): any {
    //funcao para buscar os cards no localStorage
    this.cards = JSON.parse(localStorage.getItem('cards') as any)
  }
  //funcao para buscar os cards em andamento no localStorage
  getCardsEA() {
    this.cardsEA = JSON.parse(localStorage.getItem('emAndamento') as any)
  }
  //funcao para buscar os cards Concluidosno localStorage
  getCardsC() {
    this.cardsC = JSON.parse(localStorage.getItem('concluido') as any)
  }

  //listagem inicial
  mounted() {
    this.getcards()
    this.getCardsEA()
    this.getCardsC()
  }

  //ADD CARD
  dataTextArea = {
    type: '',
    title: ''
  }

  saveLocalstorage: string = '' //variavel devolvida ao localstorage co o novo valor

  //function para ADDCARD
  addCartao(valueTextArea: string, typeCard: string) {
    this.dataTextArea.title = valueTextArea;
    //estrutura para controlar addcards
      if (typeCard == 'cards') {
        this.dataTextArea.type = 'AF';
        this.cards.push(this.dataTextArea)
        this.saveLocalstorage = JSON.stringify(this.cards)
      } else if (typeCard == 'emAndamento') {
        this.dataTextArea.type = 'EA';
        this.cardsEA.push(this.dataTextArea)
        this.saveLocalstorage = JSON.stringify(this.cardsEA)
    
      } else if (typeCard == 'concluido') {
        this.dataTextArea.type = 'C';
        this.cardsC.push(this.dataTextArea)
        this.saveLocalstorage = JSON.stringify(this.cardsC)
    
      }
      localStorage.setItem(typeCard, this.saveLocalstorage)
  }
}

//gambiarra para preencher vetor inicial

//  a: any[] = ['sssssssssssss','aaaaaaaaaaaaaaaa','bbbbbbbb']; //recebe dados do local storage convertido em array
//  b: string = ''; //variavel devolvida ao localstorage co o novo valor

//  mounted() {
//      this.b =  JSON.stringify(this.a);
//      localStorage.setItem('concluido', this.b);
//  }
</script>

<style>
button.btn-card:hover {
  background-color: #e5e5e5;
  transition: 0.3s;
}
</style>
