<template id="item-row">
    <tr>
        <td>{{ item.id + 1 }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.email }}</td>
        <td>{{ item.age }}</td>
    </tr>
</template>

<script>
export default {
    name: 'item-row',
    props: ['item'],
}
</script>

<style scoped>
    tr:nth-child(2n+1){
        background-color: rgba(0, 0, 0, 0.05);
    }
    td {
        font-weight: 300;
        padding: 10px 20px 10px 5px;

        border: 1px solid #DEE2E6;
    }
</style>
