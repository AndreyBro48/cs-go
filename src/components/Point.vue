<template>
    <span class="metka" :style="metkaStyle" v-on:click="$emit('click-point', {point})"></span>
</template>
<script>
export default {
    props: ['point'],
    // data(){
    //     return {
    //         coordsPoint:{
    //             x: 41.0,
    //             y: 42.0
    //         },
    //         sizePoint:{
    //             width: 2.1,
    //             height: 3.0 
    //         }
    //     }
    // },
    methods:{
        
    },
    computed:{
        left(){
            return this.point.coordsPoint.x - this.point.sizePoint.width / 2.0
        },
        top(){
            return this.point.coordsPoint.y - this.point.sizePoint.height / 2.0 - 0.3658537
        },
        metkaStyle() {
            console.log()
            var leftTop = `left: ${this.left}%; top: ${this.top}%;`
            var size = `width:${this.point.sizePoint.width}%; height: ${this.point.sizePoint.height}%;`
            var background
            if (this.point.type === TypePoint.StartPoint) {
                background = "background: orange;"
            } else {
                background = "background: red;"
            }
            return  leftTop + size + background
        }
        
    }
}
</script>
<style scoped>
    .m1{
        left: 39.5%;
        top: 41.5%;
        background: orange;
    }
</style>