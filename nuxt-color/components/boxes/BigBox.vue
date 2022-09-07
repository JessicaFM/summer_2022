<template>
    <div class="wrapper grid-cols-2"
        @click="saveColor">
        <div class="bigbox" :style="style">
            <transition name="fade">
                <div class="bigbox-copied" v-if="copied">
                    Copied!
                </div>
            </transition>
        </div>
        <div class="bigbox-title flex justify-end">
            <div>{{this.color}}</div>
        </div>
    </div>
</template>

<script>
import { useStore } from '~/store/myStore'

export default {
    name: 'BigBox',
    props: ['colorArray', 'colorType'],
    data() {
        return {
            copied: false
        }
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
            this.$refs.colorSelected = colorTemp
            return colorTemp
        },
        style() {
            return { "background-color": this.color ? this.color : "white" };
        },
    },
    methods: {
        saveColor: function () {
            var TempText = document.createElement("input");
            TempText.value = this.color;
            document.body.appendChild(TempText);
            TempText.select();
            
            document.execCommand("copy");
            document.body.removeChild(TempText);
            this.copied = true;
            var self = this;
            setTimeout(function() { self.copied = false }, 3000);
        }
    },
    asyncData({ $pinia }) {
        const store = useStore($pinia)
        console.log(store)
        console.log(store)
    },
}
</script>