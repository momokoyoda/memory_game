<template>
    <div id="memorygame-card">
        <v-card width="150" height="200" outlined :color="
            openState === 'opened' ? 'red'
                : openState === 'flipped' ? 'blue' : 'black'
        ">
            {{ cardNumber }}
            {{ openState }}
            <v-img max-height="150" max-width="250" :src="imageUrl"></v-img>
        </v-card>
    </div>
</template>

<script>
export default {
    props: ['openState', 'cardNumber', 'imageUrl'],
};

</script>
