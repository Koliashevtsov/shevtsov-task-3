<template id="users-table">
    <div class="users-table-container">
        <table>
            <thead>
                <item-header @sortBy="sortedBy"></item-header>
            </thead>
            <tbody>
                <item-row
                    v-for="(item, index) in items"
                    :item="item"
                    :key="index"></item-row>
            </tbody>
        </table>
    </div>
</template>

<script>
import ItemRow from './item-row/ItemRow.vue';
import ItemHeader from './item-header/ItemHeader.vue';

export default {
    name: 'users-table',
    components: {
        ItemRow,
        ItemHeader
    },
    props: ['items'],
    methods: {
        sortedBy(field, order){
            this.$emit('sortedBy', field, order);
        }
    },
    updated(){
        console.log('UsersTable updated');
    }
}

</script>

<style>
    table {
        width: 100%;
        font: 14px 'Roboto', sans-serif;

        border: 1px solid #DEE2E6;
    }
</style>
