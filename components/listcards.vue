<template>
  <div class="d-block">
    <v-card
      elevation="3"
      class="px-3 py-1 my-1"
      v-for="(list, index) in data"
      :key="index"
    >
      {{list}}
      <v-icon size="20" class="float-right"> mdi-pencil </v-icon>
      
    </v-card>
  </div>
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
import index from '../pages/index.vue'
@Component({
  components: { inserircartao, index },
})
export default class MyComponent extends Vue {
  @Prop() 
    data:any[];
  }
</script>

<style>
</style>