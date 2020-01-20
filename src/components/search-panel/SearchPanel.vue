<template id="search-panel">
    <div class="search-panel-container">
        <span class="text">Search:</span>
        <input type="text" :value="value" @input="onInput">
    </div>
</template>

<script>
export default {
    name: 'search-panel',
    props: ['value'],
    methods: {
        onInput(event){
            this.$emit('input', event.target.value)
        }
    }
}
</script>

<style scoped>
    .search-panel-container {
        margin-left: auto;
    }
    .text {
        font: 16px 'Roboto', sans-serif;
        margin-right: 5px;
    }
    input {
        padding: 4px 6px;
        border: 1px solid #DEE2E6;
        border-radius: 5px;
    }
    input:focus {
        border: 1px solid #29B0D9;
        box-shadow: 0 0 1px 3px #c4e9f5;
    }
</style>
