<template>
    <div v-if="entry" class="entry-title d-flex justify-content-between p-2">
        <div>
            <span class="text-success fs-3 fw-bold">{{day}}</span>
            <span class="mx-3 fs-3">{{month}}</span>
            <span class="mx-2 fs-4 fw-light">{{yearDate}}</span>
        </div>

        <div>
            <button class="btn btn-danger mx-2">Borrar <i class="fa fa-trash-all"></i></button>
            <button class="btn btn-primary">Subir foto <i class="fa fa-upload"></i></button>
        </div>
    </div>
    <hr>
    <div v-if="entry" class="d-flex flex-column px-3 h-75">
        <textarea v-model="entry.text" placeholder="Que sucedio hoy?"></textarea>
    </div>

    <Fab />
    <img class="img-thumbnail" src="" alt="entry-picture">
</template>
<script>
import {defineAsyncComponent} from 'vue'
import {mapGetters} from 'vuex'

import getDayMonthYear from '../helpers/getDayMonthYear'

export default {
    components: {
        Fab: defineAsyncComponent(() => import('../components/Fab.vue'))
    },
    props:{
        id:{
            type:String,
            required:true
        }
    },
    methods:{
        loadEntry() {
            const entry = this.getEntryById(this.id)
            if(! entry) return this.$router.push({name: 'no-entry'})

            this.entry = entry
        }
    },
    data(){
        return {
            entry: null
        }
    }, 
    computed: {
        ...mapGetters('journal', ['getEntryById']),
        day(){
            const { day } = getDayMonthYear(this.entry.date)
            return day
        },
        month() {
            const {month} = getDayMonthYear(this.entry.date)
            return month;
        },
        yearDate() {
            const {yearDate} = getDayMonthYear(this.entry.date)
            return yearDate
        }
    },
    created(){
        this.loadEntry()
    },
    watch: {
        id() {
            this.loadEntry()
        }
    }
}
</script>
<style lang="scss" scoped>
    textarea{
        font-size: 20px;
        border: none;
        height: 100%;

        &:focus {
            outline: none;
        }
    }

    img{
        width: 200px;
        position: fixed;
        bottom: 150px;
        right: 20px;
        box-shadow: 0px 5px 10px rgba($color: #000000, $alpha: 0.2);
    }
</style>