<template>
    <div class="">
        <h4>Pick a color</h4>
        <div class="loader mx-auto" v-if="loading"></div>
        <div class="template-box" v-else>
            <div class="grid-cols-3" v-bind:class="className">
                <input class="big-box-cloned" type="color" />
                <label class="">{{ color }}</label>
                <!-- <BigBox :colorArray="palette[0]" :colorType="colorType" /> -->
            </div>
            <template v-if="palette.length>1">  
                <BigBox :colorArray="palette[1]" :colorType="colorType" />
                <BigBox :colorArray="palette[2]" :colorType="colorType" />
                <BigBox :colorArray="palette[3]" :colorType="colorType" />
                <BigBox :colorArray="palette[4]" :colorType="colorType" />
            </template>
        </div>
        <div class="w-max pt-5">
            <button class="bg-teal500 text-white hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
            @click="fetch">
                Reload templates
            </button>
        </div>
    </div>
</template>

<script>
    import BigBox from '../boxes/BigBox.vue';

    export default {
        name: 'ColorPicker',
        components: { BigBox },
        data() {
            return {
                loading: false,
                colorType: 'rgba',
                palette: [],
                defaultColor: [255, 255, 255],
                className: 'big-box-default',
                disabledButton: false
            }
        },
        created() {
            this.palette.push(this.defaultColor);
        },
        computed: {
            color: function() {
                let colorTemp = ""
                if(this.colorType && this.colorType=='rgba') {
                    let first = (this.colorArray?this.colorArray[0]:"00")
                    let second = (this.colorArray?this.colorArray[1]:"00")
                    let third = (this.colorArray?this.colorArray[2]:"00")
                    colorTemp = "rgba(" + first + "," + second + "," + third + ")";  
                } else {
                    colorTemp = this.colorArray;  
                }
                //this.$refs.colorSelected = colorTemp
                return colorTemp
            },
        },
        methods: {
            async fetch() {
                const headers = {
                'Content-Type': 'text/plain'
                };
                this.loading = true
                this.disabledButton = true
                this.palette = await this.$axios.$post('http://colormind.io/api/', {
                        model: 'default',
                        input: [[44,43,44],"N","N","N","N"],
                    },{headers})
                    .then((response) => { 
                        this.loading = false; 
                        this.disabledButton = false;
                        this.className = 'wrapper'
                        return response.result;
                })
            },
        }
    }
</script>