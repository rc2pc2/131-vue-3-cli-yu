<script>
import axios from "axios";

export default {
    data() {
        return {
            archetypes: [],
            selectedItem : '',
            apiUrl: 'https://db.ygoprodeck.com/api/v7/archetypes.php',
        }
    },
    methods:{
        // creo un nuovo metodo in methods
        getArchetypes(){
            console.log("Chiamata per gli Archetypes API iniziata 👍");
            // effettua una chiamata GET all'indirizzo interessato della nostra API
            // axios.get(this.apiUrl)
            axios.get(this.apiUrl)
            // nel then della nostra chiamata axios (dovra' essere una arrow function)
            .then((response) => {
                    // prendiamo le informazioni che ci servono dall'api
                    console.log(response.data);
                    //👆 sostituiamo il risultato con l'array chiamato cardsList che si trova nei nostri dati reattivi
                    this.archetypes = response.data;

                })
                .catch(function (error) {
                    console.log(error);
                })
                .finally(() => {
                    this.loading = false;
                    console.log("Chiamata API per gli Archetypes terminata 💪");
                });
        },
        startArchetypeSearch(message){
            console.log(`👌 Sto emettendo l'evento archetype-search con ${message} 👌`);
            // emettere un evento custom archetype-search
            this.$emit("archetypeSearch", message);
        },
    },
    // 🧙🏻‍♂️ invochiamo il metodo costruito dall'interno di un lifecycle hook
    created(){
        this.getArchetypes();
    }
}
</script>

<template>
    <div class="form-input-group">
        <select class="form-select" v-model="selectedItem" @change="startArchetypeSearch(selectedItem)">
            <!-- per ogni archetipo -->
            <option v-for="(archetype, index) in archetypes" :key="index" :value="archetype.archetype_name">
                {{  archetype.archetype_name }}
            </option> 
        </select>
    </div>
</template>

<style scoped>
</style>