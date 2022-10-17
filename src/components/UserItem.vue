<template>
    <div class="item">
        <div class="item__date">{{user.registered}}</div>
        <div class="item__content">
            <h3>{{user.name.first}} {{user.name.last}}</h3>
            <p>{{user.about}}</p>
            <div class="dot"></div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'item',
        props: {
            user: {
                type: Object,
                required: true
            }
        },
    }
</script>

<style lang="scss">
.item {
    &:not(:first-child) {
        margin-top: 40px;
    }
    width: 100%;
    position: relative;
    &__date {
        font-size: 18px;
        color: #eaa023;
    }
    &__content {
        position: relative;
        background-color: #fff;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        border-radius: 5px;
        border: 1px solid rgba(0, 0, 0, 0.1);
        padding: 30px;
        border-radius: 5px;
        min-height: 100px;
        margin-top: 15px;
        h3 {
            font-size: 20px;
            color: #777;
            text-transform: capitalize;
            font-weight: 500;
            margin: 0;
        }
        p{
            color: #9b9b9b;
            font-size: 16px;
            font-weight: 300;
            line-height: 22px;
            margin: 10px 0 0;
        }
    }
    .dot {
        height: 20px;
        width: 20px;
        background-color: white;
        position: absolute;
        border-radius: 50%;
        border: 4px solid #0a5084;
        z-index: 200;
    }
    &:nth-child(odd) {
        padding-right: calc(50% + 70px);
        text-align: right;
        .item__content:after {
            content: '';
            position: absolute;
            width: 75px;
            height: 4px;
            background-color: #0a5084;
            top: calc(50% - 2px);
            right: -63px;
            z-index: -100;
        }
        .dot {
            top: calc(50% - 10px);
            right: -81px;
        }

        
    }
    &:nth-child(even) {
        padding-left: calc(50% + 70px);
        .item__content:after {
            content: '';
            position: absolute;
            width: 75px;
            height: 4px;
            background-color: #0a5084;
            top: calc(50% - 2px);
            left: -63px;
            z-index: -100;
        }
        .dot {
            top: calc(50% - 10px);
            left: -81px;
        }
    }
}
</style>