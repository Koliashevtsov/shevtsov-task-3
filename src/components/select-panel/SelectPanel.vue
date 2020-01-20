<template id="select-panel">
    <div class="select-panel" >
        <span class="text">Show</span>
        <select class="custom-select">
            <option value="5" @click="chooseSize">5</option>
            <option value="10" @click="chooseSize">10</option>
            <option value="15" @click="chooseSize">15</option>
            <option value="20" @click="chooseSize">20</option>
        </select>
        <span class="text">entries</span>
    </div>
</template>

<script>
export default {
    name: 'select-panel',
    methods: {
        chooseSize(event){
            const size = parseInt(event.target.value);
            this.$emit('chosenSize', size)
        }
    }
}
</script>

<style>
    .custom-select {
        margin: 0 5px;
        padding: 4px 6px;
        border: 1px solid #DEE2E6;
        border-radius: 5px;
    }
    .text {
        font: 16px 'Roboto', sans-serif;
    }
    select:focus {
        border: 1px solid #29B0D9;
        box-shadow: 0 0 1px 3px #c4e9f5;
    }
</style>
