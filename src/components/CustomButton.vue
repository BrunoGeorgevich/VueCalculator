<template>
    <div @click="onClicked(number)" :class="{Button:true, Zero:isZero, Operator: isOperator, Number: isNumber, DisabledButton: disabled}">
        <p>{{number}}</p>
    </div>
</template>

<script>
    export default {
        props: {
            number: {
                type: String,
                required: true,
                default: '-1'
            },
            disabled: {
                type: Boolean,
                required: true,
                default: false
            },
            isOperator: {
                type: Boolean,
                required: true,
                default: false
            },
            isNumber: {
                type: Boolean,
                required: true,
                default: false
            },
            isZero: {
                type: Boolean,
                required: true,
                default: false
            }
        },
        data: function () {
            return {}
        },
        methods: {
            onClicked: function(value) {
                if(!this.disabled)  this.$emit('button-was-clicked', value)
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .Button {
        display: inline-grid;
        text-align: center;
        border: 1px solid #151515;
    }
    .Zero {
        display: inline-grid;
        grid-column-start: 1;
        grid-column-end: 3;
    }

    .Number {
        background: #C5C5C5;
    }

    .Operator {
        background: #ff962e;
    }
    .DisabledButton {
        background: #595959;
    }
</style>
