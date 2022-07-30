<template>
    <div class="entry-list-cointainer">
        <div class="px-2 pt-2">
            <input v-model="term" type="text" class="form-control" placeholder="Buscar entrada">
        </div>
        <div class="entry-scrollarea">
            <Entry v-for="entry in entriesByTerm" :key="entry.id" :entry="entry"></Entry>
        </div>
    </div>
</template>
<script>
import {defineAsyncComponent} from 'vue';
import { mapGetters } from 'vuex';

export default {
    components:{
        Entry: defineAsyncComponent(() => import('./Entry.vue'))
    },
    computed:{
        ...mapGetters('journal', ['getEntriesByTern']),
        entriesByTerm() {
            return this.getEntriesByTern(this.term)
        }
    },
    data(){
        return {
            term: ''
        }
    }
}
</script>
<style lang="scss" scoped>
input{
    height: 25px;
}
.entry-list-container{
    border-right: 1px solid crimson;
    height: calc(100vh - 56px);
}

.entry-scrollarea{
    height: calc(100vh - 110px);
    overflow: scroll;
}
</style>