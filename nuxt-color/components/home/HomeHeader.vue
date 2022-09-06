<template>
    <div class="random-template content-center">
        <div class="container mx-auto flex justify-end">
            <div class="col column-wrapper">
                <button class="bg-teal500 text-white hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                @click="$fetch">
                    Reload templates
                </button>
            </div>
        </div>
        <div class="container mx-auto">
            <div class="col column-wrapper">Random temples</div>
            <div class="col column-wrapper">
                <div class="flex justify-end">
                    <div class="pr-1">
                        Mode
                    </div>
                    <div class="">
                        <select v-model="colorType"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-md focus:ring-blue-500">
                            <option disabled value="">Seleccione un elemento</option>
                            <option value="rgba" selected>RGBA</option>
                            <option value="hex">HEX</option>
                        </select>
                    </div>
                </div>
            </div>
            <div class="loader mx-auto" v-if="loading"></div>
            <div class="template-box" v-else>
                <BigBox :colorArray="palette[0]" />
                <BigBox :colorArray="palette[1]" />
                <BigBox :colorArray="palette[2]" />
                <BigBox :colorArray="palette[3]" />
            </div>
        </div>
    </div>
</template>

<script>
import BigBox from '../boxes/BigBox.vue';

export default {
    name: 'RandomPalette',
    components: { BigBox },
    data: () => ({
        palette: [],
        loading: true,
        colorType: 'rgba' // default
    }),

    async fetch() {
        const headers = {
        'Content-Type': 'text/plain'
        };
        this.loading = true
        this.palette = await this.$axios.$post('http://colormind.io/api/', {
                model: 'default'
            },{headers})
            .then((response) => { this.loading = false; return response.result;
        })
    },
    fetchOnServer: false,
    // // multiple components can return the same `fetchKey` and Nuxt will track them both separately
    fetchKey: 'site-sidebar',
}
</script>