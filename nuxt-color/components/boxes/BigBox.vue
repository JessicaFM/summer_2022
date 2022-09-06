<template>
    <div class="wrapper grid-cols-2"
        @click="saveColor">
        <div class="bigbox" :style="style"></div>
        <div class="bigbox-title flex justify-end">
            <div>{{this.color}}</div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'BigBox',
    props: ['colorArray'],
    computed: {
        color: function() {
            let first = (this.colorArray?this.colorArray[0]:"00")
            let second = (this.colorArray?this.colorArray[1]:"00")
            let third = (this.colorArray?this.colorArray[2]:"00")

            return "rgba(" + first + "," + second + "," + third + ")";  
        },
        style() {
            return { "background-color": this.color ? this.color : "red" };
        },
    },
    methods: {
        saveColor: function () {
            console.log("saving color");
            console.log(this.color);
        }
    }

}
</script>