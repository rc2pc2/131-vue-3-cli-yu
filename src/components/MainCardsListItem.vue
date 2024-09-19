<script>
export default {
    data() {
        return {
            
        }
    },
    props:{
        card: {
            type: Object,
            required: true,
        }
    }
}
</script>

<template>
    <img :src="card.card_images[0].image_url_cropped" alt="">
    <h4>
        {{ card.name }}
    </h4>
</template>

<style lang="scss" scoped>
    img{
        height: 140px;
    }
</style>