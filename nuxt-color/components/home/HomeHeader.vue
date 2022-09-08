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
                        <select v-model="colorType" @change="onChangeType($event)"
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
                <BigBox :colorArray="palette[0]" :colorType="colorType" />
                <BigBox :colorArray="palette[1]" :colorType="colorType" />
                <BigBox :colorArray="palette[2]" :colorType="colorType" />
                <BigBox :colorArray="palette[3]" :colorType="colorType" />
                <BigBox :colorArray="palette[4]" :colorType="colorType" />
            </div>
        </div>
        <div>
            <client-only>
            </client-only>
        </div>
    </div>
</template>

<script>
import { mapState } from 'pinia'
import { useTypeStore } from '~/store/myStore'
import BigBox from '../boxes/BigBox.vue';

export default {
    name: 'RandomPalette',
    components: { BigBox },
    data() {
        return {
            palette: [],
            loading: true,
            colorType: 'rgba' //default
        }  
    },
    computed: {
        ...mapState(useTypeStore, ['count'])
    },
    methods: {
        onChangeType: function(event){
            if(event.target.value == 'rgba') { this.HexToRGB() }
            else { this.RGBToHex() }
        },
        RGBToHex: function() {
            this.palette = this.palette.map(element => {
                var returnValue = {...element};

                let r = returnValue[0].toString(16)
                let g = returnValue[1].toString(16)
                let b = returnValue[2].toString(16)

                if (r.length == 1) { r = "0" + r }
                if (g.length == 1) { g = "0" + g }
                if (b.length == 1) { b = "0" + b }

                return  "#" + r + g + b
            }) 
        },
        HexToRGB: function() {
            this.palette = this.palette.map(element => {
                let r = parseInt(element.slice(1, 3), 16),
                g = parseInt(element.slice(3, 5), 16),
                b = parseInt(element.slice(5, 7), 16)

                return [r, g, b]
            })
        }
    },

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