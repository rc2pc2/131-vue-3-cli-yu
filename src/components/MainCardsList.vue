<script>
import MainCardsListItem from './MainCardsListItem.vue';

export default {
    components:{
        MainCardsListItem
    },
    data() {
        return {
            
        }
    },
    props:{
        cards: {
            type: Array,
            required: true
        }
    }
}
</script>

<template>
    <h3>
        MainCardsList con {{  cards.length }} elementi
    </h3>
    <!-- 1 : Le diamo il nome che vogliamo all'interno del self-closing tag del componente a cui vogliamo mandare la prop -->
     <!-- 2 : inseriamo il valore nella definizione della prop :nomeProp="valore" -->
      <!-- 3 : andiamo a definire le props all'interno del componente che sta per riceverle, tipizzandolo e usandolo a nostro piacimento -->
    <MainCardsListItem v-for="cardItem in cards" 
        :key="cardItem.id"
        :card="cardItem"
    />
</template>

<style scoped>
</style>