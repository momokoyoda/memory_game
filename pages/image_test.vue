<template>
    <div>
        <p v-if="!message">loading</p>
        <v-img :src="message" />
    </div>
</template>

<script>
export default {
    data() {
        return {
            message: ""
        }
    },
    async created() {
        await this.getUrl()
        // console.log('created')
    },
    methods: {
        async getUrl() {
            const response = await this.$axios.$get('https://aws.random.cat/meow')
            this.message = response.file
            // console.log('getUrl')
           

  
}
        }
    }

</script>
