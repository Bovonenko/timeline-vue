<template>
    <div class="timeline">
        <user-item 
            v-for="user in users" 
            :key="user._id"
            :user="user"
        />
    </div>
</template>

<script>
import UserItem from './UserItem.vue';
    export default {
        components: {
            UserItem
        },
        props: {
            users: {
                type: Array,
                required: true
            }
        }
    }
</script>

<style lang="scss" >
.timeline {
    display: flex;
    flex-wrap: wrap;
    position: relative;
    &::before {
        content: '';
        position: absolute;
        width: 4px;
        height: 100%;
        background-color: #0a5084;
        left: calc(50% - 2px)
    }
}

</style>