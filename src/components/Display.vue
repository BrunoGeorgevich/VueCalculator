<template>
    <div>
        <div class="DisplayData">
            <span class="DisplayDataSpan">
                <strong>
                    {{ text }}
                </strong>
            </span>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            text: {
                type: String,
                required: true,
                default:'0'
            }
        },
        data: function () {
            return {}
        }
    };
</script>

<style>
    .DisplayData {
        display: table-cell;
        height: 80%; line-height: 40px;
        width: 95%;
        margin: auto auto;
    }

    .DisplayDataSpan {
        display: inline-block;
        vertical-align: middle;
        line-height: normal;
    }
</style>
