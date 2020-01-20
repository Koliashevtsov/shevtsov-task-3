<template id="icon">
    <span style="float: right">
        <span class="icon-awesome" :class="order == 1 && labelField === activeField ? 'active' : ''">
            <font-awesome-icon :icon="arrowUp"/>
        </span>
        <span class="icon-awesome" :class="order == -1 && labelField === activeField ? 'active' : ''">
            <font-awesome-icon :icon="arrowDown"/>
        </span>
    </span>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faCaretUp, faCaretDown } from '@fortawesome/free-solid-svg-icons'

export default {
    name: 'icon',
    components: {
        FontAwesomeIcon
    },
    props: ['order', 'activeField', 'labelField'],
    data(){
        return {
            arrowUp: faCaretUp,
            arrowDown: faCaretDown
        };
    }
}
</script>

<style scoped>
    .icon-awesome {
        color: #BFBFBF;
    }
    .active {
        color: #373737;
    }
</style>
