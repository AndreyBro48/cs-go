<template>
    <div style="position:relative;height:auto;">
       
        <img :src="map.srcImage" id="elementImg"/>
        <Point 
            v-for="point in points" :key="point"
            v-bind:point="generatePointForMap(point)"
            v-on:click-point="onClickPoint"
        />
    </div>
</template>

<script>
 //v-for="met in compMets" :key="met"
 //           v-bind:met = "met"
import Point from '@/components/Point'
export default {
    props: ['map', 'points'],
    data(){
        return {
            mets: [],
            sizeOnePoint:25.0
        }
    },
    methods:{
        onClickPoint(pointData){
            this.$emit('click-point', pointData)
        },
        generatePointForMap(point){
            return {
                coordsPoint:{
                    x:point.x/this.map.widthImg*100, 
                    y:point.y/this.map.heightImg*100
                },
                sizePoint:this.sizePoint,
                type:point.type,
                id:point.id
            }
        },
    },
    components: {
       Point 
    },
    computed: {
        sizePoint() {
            return {
                width:this.sizeOnePoint/this.map.widthImg*100, 
                height:this.sizeOnePoint/this.map.heightImg*100
            }
        },
        computedPoints() {
            // var p = {
            //     coordsPoint:{x:43.678, y:51.341},
            //     size:{width:2.051, height:3.049}
            // }    
            return this.points
        }
    }
}
</script>

<style scoped>
    img {
        width: 100%;
        height: auto;
    }
    .metka{
        position:absolute;
        border-radius: 50%;
        display: inline-block;
    }
</style>