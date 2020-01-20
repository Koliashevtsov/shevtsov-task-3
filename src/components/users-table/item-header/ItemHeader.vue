<template id="item-header">
    <tr>
        <th @click="onSort" name="id">
            №
            <icon :order="order" :activeField="field" labelField="id"/>
        </th>
        <th @click="onSort" name="name">
            Name
            <icon :order="order" :activeField="field" labelField="name"/>
        </th>
        <th @click="onSort" name="email">
            E-mail
            <icon :order="order" :activeField="field" labelField="email"/>
        </th>
        <th @click="onSort" name="age">
            Age
            <icon :order="order" :activeField="field" labelField="age"/>
        </th>
    </tr>
</template>

<script>
import Icon from './icon/Icon.vue'

export default {
    name: 'item-header',
    components: {
        Icon
    },
    data(){
        return {
            order: null,
            field: ''
        };
    },
    methods: {
        onSort(event){
            console.log(event);
            const field = event.srcElement.attributes.name.value;
            if(this.field === field){
                this.order = this.order * (-1)
            } else {
                this.field = field;
                this.order = 1;
            }
            this.$emit('sortBy', this.field, this.order);
        }
    },
    updated(){
        console.log('ItemHeader, updated');
    }
}
</script>

<style scoped>
    th {
        text-align: left;
        font-weight: 400;
        padding: 10px 20px 10px 5px;

        border: 1px solid #DEE2E6;

        cursor: pointer;
    }
</style>
