<template>
    <div class="canvas">

    </div>
</template>

<script>
</script>

<style>
    .canvas{
        position:relative;
        height: calc(50vh / 2);
        display:flex;
        align-items: center;
        justify-content: center;
    }
    .canvas::before{
        position:absolute;
        content:'';
        width: 50px;
        height: 50px;
        margin:0 auto;
        background: var(--lightSalmon);
        animation: beforeAnimation 3s infinite forwards;
    }

    @keyframes beforeAnimation {
        0%{
            transform: translate(-50%,-50%);
        }
        25%{
            transform:translate(50%,-50%)
        }
        50%{
            transform: translate(50%,50%)
        }
        75%{
            transform: translate(-50%,50%);
        }
        100%{
            transform: translate(-50%,-50%);
        }
    }
</style>