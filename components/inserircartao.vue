<template>
  <div>
    <v-row>
      <v-col cols="12" md="12">
        <!-- text area  -->
        <textarea v-model="valueTextarea" style="width: 100%" class="text-add" > 
        </textarea>
        <!-- btn-confirm/close -->
       <v-btn text style="background-color: #5aac44" class="white--text px-4" @click="textAenvite()"> Adicionar cartão </v-btn> 
       <v-icon size="25" @click="closeAddCard"> mdi-close </v-icon>
       
       
      </v-col>
    </v-row>
  </div>
</template>

<style>
  .text-add{
    border: solid 1.5px #e5e5e5;
    outline: none;
    border-radius: 3px;
    padding: 0.4rem;
  }
</style>


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
  
})
export  default class MyComponent extends Vue {

  // DATA 
  valueTextarea: string = ''; // valor da text area

  closeAddCard() {
    this.$emit('closeCard')
  }

  textAenvite() {
    this.$emit('textcard', this.valueTextarea);
    this.valueTextarea = ''
  }

}
</script>