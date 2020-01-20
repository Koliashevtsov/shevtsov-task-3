<template>
    <div class="info-container">
        Showing 1 to {{ items ? items.length : 0 }} of {{ allItems.length }} entries
    </div>
</template>

<script>
export default {
    name: 'info',
    props: ['items', 'allItems']
}
</script>

<style scoped>
    .info-container {
        font: 16px 'Roboto', sans-serif;
        line-height: 35px;
    }
</style>
