<template>
    <div class="highlight-item">
        <div class="wrapper-img">
            <img
                class="highlight-img"
                :src="require('@/assets/itens/' + imageFileName)"
                :alt="altText"
            />
        </div>
        <h3>{{ title }}</h3>
        <p>{{ description }}</p>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue-demi'

export default defineComponent({
    props: {
        imageFileName: {
            type: String,
            default: 'img_item_01.jpg',
        },
        altText: {
            type: String,
            default: 'Imagem',
        },
        title: {
            type: String,
            default: 'Liquidez',
        },
        description: {
            type: String,
            default: 'Descrição',
        },
    },
})
</script>

<style scoped>
.highlight-item {
    text-align: center;
    margin-top: 40px;
    margin-left: 30px;
    margin-right: 30px;
    margin-bottom: 40px;
    width: 100%;
}
.highlight-item h3 {
    margin-top: 20px;
}
.wrapper-img {
    border-radius: 50%;
    overflow: hidden;
    width: 100px;
    height: 100px;
    margin-left: auto;
    margin-right: auto;
}
.wrapper-img img {
    width: 100%;
    height: auto;
}
@media (min-width: 768px) {
    .highlight-item {
        width: auto;
        max-width: 300px;
    }
}
</style>