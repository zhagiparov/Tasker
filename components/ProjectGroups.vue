<template>

  <div>

    <div class="wrapper display-flex-wrap">
      <div  id="new-projects"
            class='task-group'
            @drop="onDrop($event, 1)"
            @dragover.prevent
            @dragenter.prevent
            >
          Group name {{ newProjectsNumber }} (quantity)
          <div  class="task-group-card"
                v-for="item in listOne"
                :key="item.title"
                draggable
                @dragstart="startDrag($event, item)"
                >
            <span>Project {{ item.title }} Name</span>
            <span>Users working on that</span>
          </div>
      </div>
      <div  id="design"
            class='task-group'
            @drop="onDrop($event, 2)"
            @dragover.prevent
            @dragenter.prevent
            >
          Group name {{ designNumber }} (quantity)
          <div  class="task-group-card"
                v-for="item in listTwo"
                :key="item.title"
                draggable
                @dragstart="startDrag($event, item)"
                >
            <span>Project {{ item.title }} Name</span>
            <span>Users working on that</span>
          </div>
      </div>
      <div  id="setup"
            class='task-group'
            @drop="onDrop($event, 3)"
            @dragover.prevent
            @dragenter.prevent
            >
          Group name {{ setupNumber }} (quantity)
          <div  class="task-group-card"
                v-for="item in listThree"
                :key="item.title"
                draggable
                @dragstart="startDrag($event, item)"
                >
            <span>Project {{ item.title }} Name</span>
            <span>Users working on that</span>
          </div>
      </div>
      <div  id="development"
            class='task-group'
            @drop="onDrop($event, 4)"
            @dragover.prevent
            @dragenter.prevent
            >
          Group name {{ developmentNumber }} (quantity)
          <div  class="task-group-card"
                v-for="item in listFour"
                :key="item.title"
                draggable
                @dragstart="startDrag($event, item)"
                >
            <span>Project {{ item.title }} Name</span>
            <span>Users working on that</span>
          </div>
      </div>
      <div  id="testing"
            class='task-group'
            @drop="onDrop($event, 5)"
            @dragover.prevent
            @dragenter.prevent
            >
          Group name {{ testingNumber }} (quantity)
          <div  class="task-group-card"
                v-for="item in listFive"
                :key="item.title"
                draggable
                @dragstart="startDrag($event, item)"
                >
            <span>Project {{ item.title }} Name</span>
            <span>Users working on that</span>
          </div>
      </div>

    </div>

  </div>

</template>

<script>

  export default {
    data() {
      return {
        firstCard: 1,
        newProjectsNumber: 1,
        designNumber: 1,
        setupNumber: 1,
        developmentNumber: 1,
        testingNumber: 1,
        items: [
        { id: 0, title: '1', list: 1 },
        { id: 1, title: '2', list: 1 },
        { id: 2, title: '3', list: 1 },
        { id: 3, title: '4', list: 2 },
        { id: 4, title: '5', list: 2 },
        { id: 5, title: '6', list: 2 },
        { id: 6, title: '7', list: 3 },
        { id: 7, title: '8', list: 3 },
        { id: 8, title: '9', list: 3 },
        { id: 9, title: '10', list: 4 },
        { id: 10, title: '11', list: 4 },
        { id: 11, title: '12', list: 4 },
        { id: 12, title: '13', list: 5 },
        { id: 13, title: '14', list: 5 },
        { id: 14, title: '15', list: 5 },
      ]
      }
    },
    computed: {
        listOne () {
          return this.items.filter(item => item.list === 1);
        },
        listTwo () {
          return this.items.filter(item => item.list === 2)
        },
        listThree () {
          return this.items.filter(item => item.list === 3)
        },
        listFour () {
          return this.items.filter(item => item.list === 4)
        },
        listFive () {
          return this.items.filter(item => item.list === 5)
        }
    },
    mounted: function() {
          setTimeout(() => { this.countChildren() }, 0);
    },
    methods: {
    		startDrag (evt, item) {
          evt.dataTransfer.dropEffect = 'move'
          evt.dataTransfer.effectAllowed = 'move'
          evt.dataTransfer.setData('itemID', item.id)
    		},
    		onDrop (evt, list) {
    			const itemID = evt.dataTransfer.getData('itemID')
    			const item = this.items.find(item => item.id == itemID)
    			item.list = list
          setTimeout(() => { this.countChildren() }, 0)
    		},
        countChildren() {
          this.newProjectsNumber = document.getElementById('new-projects').children.length;
          this.designNumber = document.getElementById('design').children.length;
          this.setupNumber = document.getElementById('setup').children.length;
          this.developmentNumber = document.getElementById('development').children.length;
          this.testingNumber = document.getElementById('testing').children.length;
        }
    }
  }

</script>

<style scoped>

</style>
