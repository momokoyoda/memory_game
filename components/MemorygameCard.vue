<template>
<div id="memorygame-card">
<v-card
          width="150"
          height="200"
          outlined
          :color ="
          openState==='opened'? 'red'
          :openState==='flipped'? 'blue' : 'black'
      " 
>   
         {{cardNumber}}
         {{openState}}
</v-card >
</div>
</template>

<script>
export default {
    // props: ['n','ordered','closed','flipped','opened','random','flippedCard','flippedCardnumber','counter','dialog_win','dialog_lose','opened[n-1]','random[n-1]'],
    props :['n','openState','cardNumber'],
};

</script>
