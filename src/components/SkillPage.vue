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
  <div class="input-main">
    <input type="text" v-model="text">
    <button @click="addSkill()">Add</button>
    <button>Animate</button>
  </div>
  <div class="skill-list">
    <div @click="propertyDialog(index)" v-for="(skill,index) in skills" :key="index"> {{skill}}</div>
  </div>
  <!--Property Dialog-->
  <div v-if="isModalOpen" class="modal">
    <!-- Modal content -->
    <div class="modal-content">
      <span @click="isModalOpen=!isModalOpen" class="close">&times;</span>
      <div>
        <label for="name">Name</label>
        <input v-model="changeText">
        <button @click="isModalOpen=!isModalOpen">Cancel</button>
        <button @click="updateSkill()">Ok</button>
        <button @click="deleteSkill()">Delete</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.input-main {
  padding: 50px 50px 10px;
  overflow: hidden;
  display: flex;
}

input {
  width: 100%;
  padding: 2px 5px;
  border: 1px solid #555;
  outline: none;
}

.skill-list {
  padding: 0px 50px;

}

.skill-list>div {
  padding: 10px 0px;
  margin: 2px;
  border: solid 1px;
}

/*------------*/
.modal {
  display: block;
  position: fixed;
  /* Stay in place */
  z-index: 1;
  /* Sit on top */
  left: 0;
  top: 0;
  width: 100%;
  /* Full width */
  height: 100%;
  /* Full height */
  overflow: auto;
  /* Enable scroll if needed */
  background-color: rgb(0, 0, 0);
  /* Fallback color */
  background-color: rgba(0, 0, 0, 0.4);
  /* Black w/ opacity */
}

/* Modal Content/Box */
.modal-content {
  background-color: #fefefe;
  margin: 15% auto;
  /* 15% from the top and centered */
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
  /* Could be more or less, depending on screen size */
}

/* The Close Button */
.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>
