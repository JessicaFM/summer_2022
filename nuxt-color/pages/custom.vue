<template>
    <section class="container wrapper">
        <h2>Custom template</h2>
        <ColorPicker />
    </section>
</template>

<script>
    import ColorPicker from '../components/custom/ColorPicker.vue'
    export default {
        components: { ColorPicker }
    }
</script>