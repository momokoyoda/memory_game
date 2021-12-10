<template>
  <v-container class="grey lighten-5" style="height: 500px;">
    <v-row align="center">
      <v-col ml auto
        v-for="n in 8"
        :key="n"
        cols="3"  
      >
        <v-card @click="card(n)" color="black" width="150" height="200"
          outlined
          
        >
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default{
    data() {
        return {
            opened: [false, false, false, false, false, false, false, false]
        }
    },
methods: {
    card(n) {
    this.color="blue";
      }
    }
}
</script>


