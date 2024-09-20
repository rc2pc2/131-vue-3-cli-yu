<script>
    import MainCardsList from './MainCardsList.vue';
    import MainLoader from './MainLoader.vue';
    import MainSearch from './MainSearch.vue';
// cosa mi serve per realizzare una chiamata api:
// 1:  importare axios
import axios from "axios";



export default {
    components:{
        MainCardsList,
        MainLoader,
        MainSearch
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
        getCardsList( archetypeFilter = null){
            console.log("Chiamata API iniziata 👍");
            // effettua una chiamata GET all'indirizzo interessato della nostra API
            // axios.get(this.apiUrl)
            // `${this.apiUrl}?num=35&offset=0&archetype=${archetypeFilter}`
            axios.get(this.apiUrl , { // ${}
                params: {
                    num: 35,
                    offset: 0,
                    archetype: archetypeFilter
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
        },
        updateCardsList(information){
            console.log(`😶‍🌫️ E' arrivato ad AppMain l'evento archetype-search con payload: ${information} 😶‍🌫️`);
            this.getCardsList(information);
        }
    },
    // 🧙🏻‍♂️ invochiamo il metodo costruito dall'interno di un lifecycle hook
    created(){
        setTimeout(this.getCardsList, 200);
    }
}
</script>

<template>
    <h2>
        AppMain
    </h2>

    <!-- 1 : definiamo il custom event all'interno del self-closing tag del componente istanziato -->
     <!-- 2 : collego  il mio nuovo evento custom con un mio metodo -->
      <!-- 3 : definisco l'evento custom e come viene attivato nel componente figlio -->
    <MainSearch @archetype-search="updateCardsList"/>
    <MainLoader v-if="loading" />
    <!-- 1 : Le diamo il nome che vogliamo all'interno del self-closing tag del componente a cui vogliamo mandare la prop -->
     <!-- 2 : inseriamo il valore nella definizione della prop :nomeProp="valore" -->
      <!-- 3 : andiamo a definire le props all'interno del componente che sta per riceverle, tipizzandolo e usandolo a nostro piacimento -->
    <MainCardsList v-else :cards="cardsList" />
</template>

<style scoped>
</style>