<template>
  <v-container class="grey lighten-5" style="height: 500px">
    <v-row align="center">
      <v-col ml auto v-for="n in 8" :key="n" cols="3">
        <v-card
          @click="card(n)"
          width="150"
          height="200"
          outlined
          :color="
            opened[n - 1] === 'opened' || opened[n - 1] === 'flipped'
              ? 'blue'
              : 'black'
          "
        >       
          {{ random[n-1]}}
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
const shuffle = ([...array]) => {
  for (let i = array.length - 1; i >= 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
  return array;
}
export default {
  data() {
    const ordered=[1,1,2,2,3,3,4,4]
    return {
      // カードのじょうたいは
      // closed: 裏
      // flipped: 一時的に表
      // opened: 表
      opened: [
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
      ],
      random:shuffle(ordered), 
    }
  },
  methods: {
    card(n) {
      if (this.opened[n - 1] === 'closed') {
        this.opened.splice(n - 1, 1, 'flipped')
      } else if (this.opened[n - 1] === 'flipped') {
        this.opened.splice(n - 1, 1, 'closed')
      }

      
      if(this.opened.filter(cardStatus => cardStatus === 'flipped').length===2){
        this.opened.forEach((cardStatus, idx) => {
          if (cardStatus==='flipped') {
            this.opened.splice(idx, 1, 'closed')
          }
  
         // return cardStatus === 'flipped'
        })

       // this.opened.splice(flippedIdx, 1, 'closed')
       // this.opened.splice(n-1, 1, 'closed')
      }
      
    },
  },
}
</script>
