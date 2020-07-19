<template>
  <div id="app">
    <!-- <h1>Todo application</h1> -->
    <!-- <AddTodo /> -->
    <!-- <hr>  -->
    <div v-if="showVideo" v-on:click="showVideo = false" class="video_div">
      <iframe class="video" height="720" src="https://www.youtube.com/embed/E6yoT6sL_Uo?autoplay=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
      <!-- <video src="@/assets/v.mp4" controls autoplay muted/> -->
      <span class="close_video"/>
    </div>
    <Map v-if="!showVideo"
      v-bind:map="map"
      v-bind:points="paintPoints"
      @click-point="onClickPoint"
    />
    <!-- <TodoList 
      v-bind:todos = "todos"
      @remove-todo = "removeTodo"
    /> -->
    
  </div>
</template>

<script>
import TodoList from '@/components/ToDoList'
import AddTodo from '@/components/AddTodo'
import Map from '@/components/Map'
export default {
  created(){
    this.points = this.endPoints
  },
  name: 'App',
  data(){
    return {
      showVideo:false,
      nowShow:TypePoint.EndPoint,
      map:{
        id: 1,
        name: "Mirage",
        srcImage: 'https://csspy.com/wp-content/uploads/2018/08/Mirage-Map-Top-Down-Overview.jpg',
        stepPxel: 1.0,
        widthImg: 1218,
        heightImg: 820
      },
      keyPositions:[{
          id:1,x:501,y:351
        }
      ],
      points:[],
      startPoints:[{
        id:2, type:TypePoint.StartPoint, idEndPoint:2, x:744, y:263
      }],
      endPoints:[
        {id: 1, type:TypePoint.EndPoint, x:501, y:351}
      ],
      todos: [
        {id: 1, title: 'Купить 1', completed: false},
        {id: 2, title: 'Купить 2', completed: false},
        {id: 3, title: 'Купить 3', completed: false}
      ]
    }
  },
  
  components: {
   TodoList, AddTodo, Map
  },
  methods:{
    getStartPoints(endId){
      return this.startPoints
    },
    getEndPointsById(id){
      return this.endPoints.filter(t=> t.id === id)[0]
    },
    onClickPoint(pointData){
      var point = pointData.point
      if (point.type === TypePoint.EndPoint){
        this.points = []
        if (this.nowShow === TypePoint.EndPoint){
          this.points.push(this.getEndPointsById(point.id))
          this.points = this.points.concat(this.getStartPoints(point.id))
          this.nowShow = TypePoint.StartPoint
        } else if (this.nowShow === TypePoint.StartPoint) {
          this.points = this.points.concat(this.endPoints)
          this.nowShow = TypePoint.EndPoint
        }
      } else if (point.type === TypePoint.StartPoint) {
        this.showVideo = true
      }
    },
    removeTodo(id){
      this.todos = this.todos.filter(t => t.id !== id)
    }
  },
  computed:{
    paintPoints(){
      return this.points
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.video_div{
  position:relative;
  height:800px;
}
.video{
  width: 100%;
  height: 60%;
}
.close_video{
  position:absolute;
  right: 5%;
  top: 5%;
  border-radius: 50%;
  height: 30px;
  width: 30px;
  background: url(./assets/close.png);
  background-size: 100%;
  display: inline-block;
    /* pointer-events: all;
    cursor: pointer;
    position: fixed;
    top: 10px;
    right: 10px;
    height: 30px;
    width: 30px;
    background-image: url(./assets/close.png);
    background-size: contain; */
}
</style>
