
<template>
  <div class="d-block">
    <v-card
      elevation="3"
      class="px-3 py-1 my-1"
      v-for="(list, index) in data"
      :key="index"
    >
      {{ list.title }}
      
      <!-- Dropdown -->
      <v-menu offset-y>
        <template v-slot:activator="{ on, attrs }">
          <v-icon
            @click="alterList(list)"
            class="float-right ml-2"
            color="#DCDCDC"
            dark
            v-bind="attrs"
            v-on="on"
          >
            mdi-arrow-right
          </v-icon>
        </template>
        <v-list v-for="(item, index) in items" :key="index">
          <v-list-item class="list-items"> {{ item.title }} </v-list-item>
        </v-list>
      </v-menu>

      <v-icon
        class="float-right ml-2"
        color="#DCDCDC"
        dark
        v-bind="attrs"
        v-on="on"
      >
        mdi-delete-outline
      </v-icon>
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
  @Prop({ required: true, default: [] }) data!: any[]

  items: any[] = [
    { type: 'AF', title: 'A fazer' },
    { type: 'EA', title: 'Em andamento' },
    { type: 'C', title: 'Concluido' },
  ]

  alterList(type: string) {
    console.log(type);
    let expression: string = type;

    switch (expression) {
      case 'AF': {
        console.log('type AF');
        break
      }
      case 'EA': {
        console.log('type EA');
        break
      }
      case 'C': {
        console.log('type C');
        break
      }

      default: {
        //statements;
        break
      }
    }
  }
}
</script>


<style>
i.hover-delete:hover {
  color: red;
}

i.hover-arrow:hover {
  color: orange;
}
.list-items:hover {
  background-color: #dcdcdc;
}

.v-list {
  padding: 0px;
}
</style>