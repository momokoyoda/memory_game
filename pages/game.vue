<template>
  <v-container class="grey lighten-5" style="height: 500px">
    <v-row>
     <!-- <v-col style="color: black">
        さいごにクリックしたかーどは　{{lastClickCard}}
      </v-col>
      -->
    </v-row>
    <v-row align="center">
      <v-col ml auto v-for="n in 8" :key="n" cols="3">
        <memorygame-card  
          @click.native="card(n)"
          :openState="opened[n-1]"
          :cardNumber="random[n-1]">
        </memorygame-card>
      </v-col>
    </v-row>

    <!-- モーダルウィンドウ -->
    <div class="text-center">
   <!-- 成功したとき -->
    <v-dialog
      v-model="dialog_win"
      width="500"
    >
      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          You Win
        </v-card-title>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="$router.push('/')"
          >
            Back
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    
    <!-- 失敗したとき -->
     <v-dialog
      v-model="dialog_lose"
      width="500"
    >
      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          You Lose
        </v-card-title>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="reset"
          >
            Try Again
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
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
     // lastClickCard: null,
      flippedCard:null,
      flippedCardnumber:null,
      counter:null,
      dialog_win:false,
      dialog_lose:false,
      
    }
  },
  methods: {
    reset(){
      const ordered=[1,1,2,2,3,3,4,4]
// カードのじょうたいは
      // closed: 裏
      // flipped: 一時的に表
      // opened: 表
      this.opened= [
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
      ]
      this.random=shuffle(ordered)
      this.flippedCard=null
      this.flippedCardnumber=null
      this.counter=null
      this.dialog_lose=false
  },
    card(n) {
       console.log("yes")
      var counter =0
     // this.lastClickCard = this.random[n - 1]
      if (this.opened[n - 1] === 'closed') {
        this.opened.splice(n - 1, 1, 'flipped')
       // this.flippedCard= this.random[n-1]
        //this.flippedCardnumber = n-1;  
      } else if (this.opened[n - 1] === 'flipped') {
        this.opened.splice(n - 1, 1, 'closed')
        this.flippedCard= null
      }      
      if(this.opened.filter(cardStatus => cardStatus === 'flipped').length===1){
        this.flippedCard= this.random[n-1]
        this.flippedCardnumber = n-1;  
      }
      if(this.opened.filter(cardStatus => cardStatus === 'flipped').length===2)
      {
        this.counter++;
        console.log(this.counter)
        this.opened.forEach((cardStatus, idx) => {
           if(this.flippedCard===this.random[n-1]){
             this.opened.splice(n - 1, 1, 'opened')
             this.opened.splice(this.flippedCardnumber, 1, 'opened')

           }
           else{
             this.opened.splice(n - 1, 1, 'closed')
             this.opened.splice(this.flippedCardnumber, 1, 'closed')
           }

         // if (cardStatus==='flipped') {
           // this.opened.splice(idx, 1, 'closed')
          //}
  
         // return cardStatus === 'flipped'
        })
      }
       var openCard =0
       openCard = this.opened.filter(cardStatus => cardStatus === 'opened').length
       if(openCard===8){
         this.dialog_win=true
         console.log("you win")
         
       }
       else if(this.counter===8&&openCard<8){
         this.dialog_lose=true
         console.log("you lose")
       }
      
           
          
       // this.opened.splice(flippedIdx, 1, 'closed')
       // this.opened.splice(n-1, 1, 'closed')

      },
    },
};

</script>
