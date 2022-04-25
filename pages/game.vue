<template>
  <v-container class="grey lighten-5" style="height: 500px">
    <v-row>
    </v-row>
    <v-row align="center">
      <v-col ml auto v-for="n in 8" :key="n" cols="3">
        <memorygame-card @click.native="card(n)" :openState="opened[n - 1]" :cardNumber="random[n - 1]"
          :imageUrl="urlList[random[n - 1] - 1]">
        </memorygame-card>
      </v-col>
    </v-row>

    <!-- モーダルウィンドウ -->
    <div class="text-center">
      <!-- 成功したとき -->
      <v-dialog v-model="dialog_win" width="500">
        <v-card>
          <v-card-title class="text-h5 grey lighten-2">
            You Win
          </v-card-title>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" text @click="$router.push('/')">
              Back
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>

      <!-- 失敗したとき -->
      <v-dialog v-model="dialog_lose" width="500">
        <v-card>
          <v-card-title class="text-h5 grey lighten-2">
            You Lose
          </v-card-title>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" text @click="reset">
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
    const ordered = [1, 1, 2, 2, 3, 3, 4, 4]
    // const urlList=["","","","","","","",""]
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
      random: shuffle(ordered),
      flippedCard: null,
      flippedCardnumber: null,
      counter: null,
      dialog_win: false,
      dialog_lose: false,
      urlList: ["", "", "", ""]
    }
  },
  async created() {
    const image1 = await this.$axios.$get('https://aws.random.cat/meow').file
    const image2 = await this.$axios.$get('https://aws.random.cat/meow').file
    const image3 = await this.$axios.$get('https://aws.random.cat/meow').file
    const image4 = await this.$axios.$get('https://aws.random.cat/meow').file

    this.urlList = [image1, image2, image3, image4]
  },

  methods: {
    reset() {
      const ordered = [1, 1, 2, 2, 3, 3, 4, 4]
      this.opened = [
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
        'closed',
      ]
      this.random = shuffle(ordered)
      this.flippedCard = null
      this.flippedCardnumber = null
      this.counter = null
      this.dialog_lose = false
    },
    card(n) {
      // console.log("yes")


      var counter = 0
      // this.lastClickCard = this.random[n - 1]
      if (this.opened[n - 1] === 'closed') {
        this.opened.splice(n - 1, 1, 'flipped')
        // this.flippedCard= this.random[n-1]
        //this.flippedCardnumber = n-1;  
      } else if (this.opened[n - 1] === 'flipped') {
        this.opened.splice(n - 1, 1, 'closed')
        this.flippedCard = null
      }
      //this.image.splice(n - 1, 1, UrlList)

      if (this.opened.filter(cardStatus => cardStatus === 'flipped').length === 1) {
        this.flippedCard = this.random[n - 1]
        this.flippedCardnumber = n - 1;
      }
      if (this.opened.filter(cardStatus => cardStatus === 'flipped').length === 2) {
        this.counter++;
        console.log(this.counter)
        this.opened.forEach((cardStatus, idx) => {
          if (this.flippedCard === this.random[n - 1]) {
            this.opened.splice(n - 1, 1, 'opened')
            this.opened.splice(this.flippedCardnumber, 1, 'opened')

          }
          else {
            setTimeout(() => {
              this.opened.splice(n - 1, 1, 'closed')
              this.opened.splice(this.flippedCardnumber, 1, 'closed')
            }, 1000)
          }
        })
      }
      var openCard = 0
      openCard = this.opened.filter(cardStatus => cardStatus === 'opened').length
      if (openCard === 8) {
        this.dialog_win = true
        console.log("you win")

      }
      else if (this.counter === 8 && openCard < 8) {
        this.dialog_lose = true
        console.log("you lose")
      }
    },


  },
};

</script>
