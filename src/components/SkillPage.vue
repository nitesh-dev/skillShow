<script setup lang="ts">
import { Ref, ref } from 'vue'

const count = ref(0)
const text = ref("")
const changeText = ref("")
const skills: Ref<string[]> = ref([])
const isModalOpen = ref(false)
var selectedIndex = -1;


function addSkill() {
  var isSame = false;
  skills.value.forEach((e) => {
    if (e === text.value) {
      isSame = true
      return
    }
  })
  if (!isSame) {
    skills.value.push(text.value)
  }
  console.log(skills.value)

}

function propertyDialog(i: number) {
  selectedIndex = i
  changeText.value = skills.value[selectedIndex]
  isModalOpen.value = !isModalOpen.value
  selectedIndex = selectedIndex
}
function deleteSkill() {
  skills.value.splice(selectedIndex, 1)
  isModalOpen.value = !isModalOpen.value
}
function updateSkill() {
  skills.value[selectedIndex] = changeText.value
  isModalOpen.value = !isModalOpen.value

}
</script>

<template>

  <!-- input area -->
  <div class="input-main">
    <input type="text" v-model="text">
    <button @click="addSkill()">Add</button>
    <button>Animate</button>
  </div>

  <!-- skill list -->
  <div class="skill-list">
    <div @click="propertyDialog(index)" v-for="(skill,index) in skills" :key="index"> {{skill}}</div>
  </div>


  <!--Property Dialog-->
  <div v-if="isModalOpen" class="modal">
    <!-- Modal content -->
    <div class="modal-content">
      <div>
        <label for="name">Name:</label>
        <input v-model="changeText">
        <button @click="isModalOpen=!isModalOpen">Cancel</button>
        <button @click="updateSkill()">Ok</button>
        <button @click="deleteSkill()">Delete</button>
        <span @click="isModalOpen=!isModalOpen" class="close">&times;</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  font-size: 16px;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.input-main {
  padding: 50px 50px 10px;
  overflow: hidden;
  display: flex;
}

.input-main input {
  width: 100%;
  padding: 8px 20px;
  background-color: rgb(236, 236, 236);
  border: none;
  border-radius: 8px 0 0 8px;
  outline: none;
}

.input-main button {
  padding: 0 15px;
  border: none;
  background-color: rgb(0, 153, 255);
  font-weight: 400;
  color: white;
}

.input-main button:hover{
  opacity: 0.8;
}

.input-main button:last-child{
  border-radius: 0 8px 8px 0;
}




/* skill list */
.skill-list {
  padding: 20px 50px;

}

.skill-list>div {
  font-weight: 400;
  padding: 10px 20px;
  margin: 8px 0;
  background-color: rgb(241, 241, 241);
  border-radius: 8px;
  color: rgb(104, 104, 104);
}



/*---- model box -------*/
.modal {
  display: flex;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.4);
}

/* Modal Content/Box */
.modal-content {
  background-color: #fefefe;
  margin: auto auto;
  padding: 40px 20px;
  border: 1px solid #888;
  width: 70%;
  border-radius: 8px;
}

.modal-content>div{
  display: flex;
  align-items: center;
  vertical-align: middle;
}

.modal-content label{
  margin-right: 10px;
}

.modal-content input{
  width: 100%;
  padding: 8px 20px;
  background-color: rgb(236, 236, 236);
  border: none;
  border-radius: 8px 0 0 8px;
  outline: none;
}

.modal-content button {
  padding: 8px 15px;
  border: none;
  background-color: rgb(0, 153, 255);
  font-weight: 400;
  color: white;
}

.modal-content button:hover{
  opacity: 0.8;
}

.modal-content div :nth-last-child(2){
  border-radius: 0 8px 8px 0;
}


.modal-content .close {
  margin-left: 20px;
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.modal-content .close:hover,
.modal-content .close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>
