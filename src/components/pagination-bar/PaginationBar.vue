<template id="pagination-bar">
    <div class="pagination-container">
        <button type="button" @click="setPrevious" class="pagination-item"
            :disabled="activePage === 1">Previous</button>
        <ul class="pagination-items">
            <li v-for="item in items" :key="item" >
                <span class="pagination-item" @click="changePage"
                    :class="isActivePage(item) ? 'active' : ''">
                    {{ item }}
                </span>
            </li>
        </ul>
        <button type="button" name="button" @click="setNext" class="pagination-item"
            :disabled="activePage === items">Next</button>
    </div>
</template>


<script>
export default {
    name: 'pagination-bar',
    props: ['items', 'activePage'],
    methods: {
        changePage(event){
            const numb = parseInt(event.srcElement.textContent);
            this.$emit('changedPage', numb);
        },
        setPrevious(){
            this.$emit('changedPage', this.activePage - 1)
        },
        setNext(){
            this.$emit('changedPage', this.activePage + 1)
        },
        isActivePage(item){
            return this.activePage === item;
        },
        isDisabledButton(){
            return this.activePage === 1 || this.activePage === this.items;
        }
    }
}
</script>

<style scoped>
    .pagination-container {
        display: flex;
        flex-flow: row;
        margin-left: auto;

        font: 14px 'Roboto', sans-serif;
        height: 35px;
    }
    .pagination-items {
        display: flex;
        flex-flow: row;
    }
    .pagination-item {
        display: inline-block;
        padding: 0 12px;
        line-height: 35px;
        height: 100%;
    }
    .pagination-item:hover:not(.active) {
        cursor: pointer;
        background-color: #f2f2f2;
    }
    .active {
        background-color: #4285f4;
        border-radius: 1px;
        box-shadow: 0 2px 5px 0 rgba(0,0,0,0.16),0 2px 10px 0 rgba(0,0,0,0.12);
        cursor: pointer;
    }
    .disabled {
        opacity: 0.6;
        cursor: not-allowed;
    }
    button {
        background-color: white;
        border: none;
        font: 14px 'Roboto', sans-serif;
    }
</style>
