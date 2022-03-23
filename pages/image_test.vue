<template>
    <h2>Image test</h2>
</template>
<script>
export default {
    created() {
        const response = this.$axios.$get('https://aws.random.cat/meow')
        console.log(response)
    }
}
</script>