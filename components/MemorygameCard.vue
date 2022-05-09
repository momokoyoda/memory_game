<template>
    <div id="memorygame-card">
        <v-card width="150" height="200" outlined :color="
            openState === 'opened' ? 'red'
                : openState === 'flipped' ? 'blue' : 'black'
        ">
            {{ cardNumber }}
            {{ openState }}
            <v-img v-show="openState !== 'closed'" height="150" width="200" :src="imageUrl"></v-img>
        </v-card>
    </div>
</template>

<script>
export default {
    props: ['openState', 'cardNumber', 'imageUrl'],
};

</script>
