<template>
  <v-app dark>
    <v-app-bar
      :clipped-left="true"
      fixed
      app
      color="#026aa7"
      height="40px"
      class="py-2"
    >
      <!-- GRUPO DE BOTES left -->
      <div class="row" align="center">
        <v-btn class="white--text" color="hsla(0,0%,100%,.24)">
          <v-icon> mdi-apps </v-icon>
        </v-btn>

        <v-btn class="white--text" color="hsla(0,0%,100%,.24)">
          <v-icon> mdi-home </v-icon>
        </v-btn>

        <v-btn class="white--text" color="hsla(0,0%,100%,.24)">
          <v-icon class="px-2">mdi-application </v-icon>
          <h5 class="mr-5">Quadros</h5>
        </v-btn>

        <v-text-field
          class="heigth-bnt-nav"
          append-icon="mdi-magnify"
          label="Search"
          hide-details
          placeholder="Placeholder"
          solo
        ></v-text-field>

        <!-- \GRUPO DE BOTES left-->

        <v-spacer />

        <!-- BOTOES LATERAL direita -->
        <div>
          <v-btn class="white--text" color="hsla(0,0%,100%,.24)">
            <v-icon> mdi-plus-box-outline </v-icon>
          </v-btn>

          <v-btn class="white--text" color="hsla(0,0%,100%,.24)">
            <v-icon> mdi-information-outline </v-icon>
          </v-btn>

          <v-btn class="white--text" color="hsla(0,0%,100%,.24)">
            <v-icon class="px-2">mdi-bell</v-icon>
          </v-btn>
        </div>
      </div>
    </v-app-bar>
    <!-- Fim navbar ========================================================= -->
    <!-- V-mai =============== -->
    <v-main style="background-color: #3372AA">
      <!-- Menus botoes lado direito-->
      <div class="row ml-2 py-2">
        <v-btn color="hsl(195, 56%, 50%)" class="py-5 px-0">
          <v-icon class="px-1 white--text"> mdi-application </v-icon>
          <h5 class="mr-2 white--text">Quadros</h5>
          <v-icon class="white--text mr-2">mdi-arrow-down-thick </v-icon>
        </v-btn>

        <h3 class="white--text px-2 my-auto">Nome da tarefa</h3>

        <v-btn color="hsl(195, 56%, 50%)" class="py-5 px-0" min-width="40px">
          <v-icon class="white--text mx-auto">mdi-star-outline </v-icon>
        </v-btn>
        <v-spacer />
        <!-- \Menus botoes lado direito-->

        <!-- botoes lado direito menu2-->
        <v-btn color="hsl(195, 56%, 50%)" class="py-5 px-0">
          <v-icon class="px-1 white--text"> mdi-calendar-month </v-icon>
          <h5 class="mr-2 white--text">Calendario</h5>
        </v-btn>

        <v-btn color="hsl(195, 56%, 50%)" class="py-5 px-0 mr-5" min-width="40px">
          <v-icon class="white--text mx-auto">mdi-animation-outline </v-icon>
        </v-btn>

        <!-- \botoes lado direito menu2-->
      </div>

      <!-- \Menus -->
      <!-- rederização de componentes -->
        <nuxt />
    </v-main>


  </v-app>
</template>

<script lang="ts">

import {
  Component,
  Inject,
  Model,
  Prop,
  Provide,
  Vue,
  Watch
} from "nuxt-property-decorator"

import inserircartao from "../components/inserircartao.vue";



@Component({
  components: { inserircartao },
})
export  default class MyComponent extends Vue {

}


</script>
<style>
.v-btn:not(.v-btn--round).v-size--default {
  height: 2rem;
  min-width: 2rem;
  padding: 0px;
  margin-right: 0.3rem;
}

/* CLASSE PADRAO VUETIFY */
.v-input__slot {
  align-items: center;
  color: inherit;
  display: flex;
  margin-bottom: 8px;
  min-height: 2rem;
  position: relative;
  transition: 0.3s cubic-bezier(0.25, 0.8, 0.5, 1);
  width: 30%;
}
</style>
