<template>
    <div class="app">
        <div class="top-panel">
            <select-panel @chosenSize="setSize"></select-panel>
            <search-panel v-model="searchTerm"></search-panel>
        </div>
        <users-table
            :items="usersData"
            @sortedBy="sortList"></users-table>
        <div class="bottom-panel">
            <info :items="usersData" :allItems="filterList"></info>
            <pagination-bar
                :items="pagesCount"
                :activePage="currentPage"
                @changedPage="setCurrentPage"></pagination-bar>
        </div>


    </div>
</template>

<script>

import usersList from './users-data.js';

import SearchPanel from './components/search-panel/SearchPanel.vue';
import SelectPanel from './components/select-panel/SelectPanel.vue';
import UsersTable from './components/users-table/UsersTable.vue';
import Info from './components/info/Info.vue';
import PaginationBar from './components/pagination-bar/PaginationBar.vue'

export default {
    name: 'app',
    components: {
        SearchPanel,
        SelectPanel,
        UsersTable,
        Info,
        PaginationBar
    },
    data(){
        return {
            searchTerm: '',
            usersData: null,
            tableSize: 5,
            pagesCount: null,
            currentPage: 1 // i initializate this property in this component but not in PaginatorBar because i do not want to create and pass special method (which return currentPage=1 after set another page size) to PaginatorBar
        };
    },
    computed: {
        filterList(){
            return this.searchItems(usersList, this.searchTerm);
        }
    },
    methods: {
        searchItems(items, search){
            if(search.length === 0){
                return items;
            }
            return items.filter((item) => item.name.indexOf(search) > -1);
        },
        sortList(field, order){
            console.log(`field > ${field}, order > ${order}`);
            this.filterList.sort((a, b) => a[field] > b[field] ? 1 * order : -1 * order)
            console.log(this.filterList);
            this.getUsersSlice(this.tableSize, this.currentPage)
        },
        getUsersSlice(size, curPage){
            const startIdx = (curPage - 1) * size;
            const endIdx = startIdx + size;
            console.log(`startIdx === ${startIdx}`);
            console.log(`endIdx === ${endIdx}`);
            this.usersData = this.filterList.slice(startIdx, endIdx)
        },
        getPagesCount(tableSize){
            // in this method I calculate how many pagesCount I get
            // basis on tableSize
            const count = this.filterList.length / tableSize;
            this.pagesCount = Math.ceil(count)
        },
        setSize(size){
            this.tableSize = size;

            // before call next method I set this.currentPage in 1
            this.currentPage = 1;
            // in order to return table in beginning state
            this.getUsersSlice(this.tableSize, this.currentPage)
        },
        setCurrentPage(value){
            this.currentPage = value;
        }
    },
    mounted(){
        console.log('App mounted');
        // set data in our table from 'users-data.js'
        // accordind to tableSize
        this.getUsersSlice(this.tableSize, this.currentPage)

        // calculate count of pages in paginator
        console.log(`this.filterList.length, ${this.filterList.length}`);
        this.getPagesCount(this.tableSize);
        console.log(`this.pagesCount, ${this.pagesCount}`);

    },
    watch: {
        tableSize(value){
            // calculate count of pages in paginator
            console.log(this.filterList.length);
            this.getPagesCount(value);
            console.log(this.pagesCount);
        },
        currentPage(value){
            console.log(`currentPage ${value}`);
            this.getUsersSlice(this.tableSize, value)
        },
        searchTerm(){
            this.currentPage = 1
            this.getUsersSlice(this.tableSize, this.currentPage)
        },
        filterList(){
            this.getPagesCount(this.tableSize);
            // this.getUsersSlice(this.tableSize, this.currentPage)
        }
    }
}
</script>

<style>
    .app {
        width: 960px;
        margin: auto;
        margin-top: 20px;
    }
    .top-panel {
        display: flex;
        flex-flow: row;
        padding-bottom: 20px;
    }
    .bottom-panel {
        display: flex;
        flex-flow: row;
        padding-top: 30px;
    }
</style>
