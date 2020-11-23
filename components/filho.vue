
<template>
 <div>
     <v-btn @click="mandaPropai()"> <h1> Sou um filho ó</h1> </v-btn>
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
  Watch
} from "nuxt-property-decorator"


@Component({
  components: {  },
})
export  default class MyComponent extends Vue {

    propai:string = 'teste comunicação'

    mandaPropai() {
        this.$emit('opai', this.propai);
    }

}


</script>

<style>

</style>
