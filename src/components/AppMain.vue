<script>
    import MainCardsList from './MainCardsList.vue';
    import MainLoader from './MainLoader.vue';
// cosa mi serve per realizzare una chiamata api:
// 1:  importare axios
import axios from "axios";



export default {
    components:{
        MainCardsList,
        MainLoader
    }, 
    data() {
        return {
            // creo un nuovo dato reattivo, che sia un array vuoto chiamato cardsList
            cardsList : [],
            // creo un nuovo dato reattivo, che sia una stringa contentente l'indirizzo dell'api 
            apiUrl: "https://db.ygoprodeck.com/api/v7/cardinfo.php",
            // TODO => inserire sintassi params con axios
            loading: true,
        }
    },
    methods: {
        // creo un nuovo metodo in methods
        getCardsList(){
            console.log("Chiamata API iniziata 👍");
            // effettua una chiamata GET all'indirizzo interessato della nostra API
            // axios.get(this.apiUrl)
            axios.get(this.apiUrl, {
                params: {
                    num: 35,
                    offset: 0,
                }
            })
            // nel then della nostra chiamata axios (dovra' essere una arrow function)
            .then((response) => {
                    // prendiamo le informazioni che ci servono dall'api
                    console.log(response.data.data);
                    //👆 sostituiamo il risultato con l'array chiamato cardsList che si trova nei nostri dati reattivi
                    this.cardsList = response.data.data;
                })
                .catch(function (error) {
                    console.log(error);
                })
                .finally(() => {
                    this.loading = false;
                    console.log("Chiamata API terminata 💪");
                });
        }
    },
    // 🧙🏻‍♂️ invochiamo il metodo costruito dall'interno di un lifecycle hook
    created(){
        setTimeout(this.getCardsList, 2000);
    }
}
</script>

<template>
    <h2>
        AppMain
    </h2>
    <MainLoader v-if="loading" />
    <!-- 1 : Le diamo il nome che vogliamo all'interno del self-closing tag del componente a cui vogliamo mandare la prop -->
     <!-- 2 : inseriamo il valore nella definizione della prop :nomeProp="valore" -->
      <!-- 3 : andiamo a definire le props all'interno del componente che sta per riceverle, tipizzandolo e usandolo a nostro piacimento -->
    <MainCardsList v-else :cards="cardsList" />
</template>

<style scoped>
</style>