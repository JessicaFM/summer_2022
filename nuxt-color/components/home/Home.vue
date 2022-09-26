<template>
    <section class="container content-center mx-auto">
        <div class="wrapper">
            Custom
            <RandomPalette />
        </div>
    </section>
</template>

<script>
    import RandomPalette from './RandomPalette.vue';

    export default {
        components: { RandomPalette }
    }
</script>