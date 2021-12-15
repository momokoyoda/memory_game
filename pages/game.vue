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
          {{ opened[n - 1] }}
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      // カードのじょうたいは
      // closed: 裏
      // flipped: 一時的に表
      // opened: 表
      opened: [
        'flipped',
        'closed',
        'opened',
        'flipped',
        'closed',
        'closed',
        'closed',
        'closed',
      ],
    }
  },
  methods: {
    card(n) {
      if (this.opened[n - 1] === 'closed') {
        this.opened.splice(n - 1, 1, 'flipped')
      } else if (this.opened[n - 1] === 'flipped') {
        this.opened.splice(n - 1, 1, 'closed')
      }
    },

    // if(opened[n-1]==='closed') opened[n-1]='flipped';
    // else if(opened[n-1]==='flipped') opened[n-1]='closed';
  },
}
</script>
