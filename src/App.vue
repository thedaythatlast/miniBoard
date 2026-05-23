// caveat: strict type checking when the app is built should be disabled currently in tsconfig.app.json

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import './metadata/meta.ts'

const CELL_SIZE = 10 // size of each drawn pixel

const canvas = ref(null)
let ctx

const mouseDown = ref(false) // tracking if the mouse button is being held down or not

const grid = ref<(string | null)[]>(
  JSON.parse(localStorage.getItem('grid') ?? 'null') ?? new Array(80 * 60).fill("white")
)

const colors = [
  { color: "white", hover: "#e0e0e0" },
  { color: "red", hover: "#ff6b6b" },
  { color: "blue", hover: "#6bbcff" },
  { color: "yellow", hover: "#fff9b0" },
  { color: "green", hover: "#7dff9b" },
  { color: "orange", hover: "#ffb86b" },
  { color: "cyan", hover: "#cfffff" },
  { color: "pink", hover: "#ff9ed2" },
  { color: "purple", hover: "#c792ff" }
]
const hovering = ref(null) // is the mouse hovering on the color buttons?
const color = ref("red") // this variable directly determines the color of the drawer

let saveTimer // storing timeouts



onMounted(() => {
  const el = canvas.value!;
  el.width = 800;
  el.height = 600;
  ctx = el.getContext('2d')!;
  loadCanvas();
})

// load localstorage data to the canvas
function loadCanvas() {
  grid.value.forEach((c, i) => {
    if (c) drawPixel(i % 80, Math.floor(i / 80), c)
  }) 
}

function drawPixel(x: number, y: number, color: string) {
  const gap = 1;
  ctx.fillStyle = color;
  ctx.fillRect(x*CELL_SIZE + gap, y*CELL_SIZE + gap, CELL_SIZE - gap, CELL_SIZE - gap);
  grid.value[y * 80 + x] = color  ;
  if (saveTimer) clearTimeout(saveTimer)
  saveTimer = setTimeout(() => {
    localStorage.setItem('grid', JSON.stringify(grid.value))
  }, 500)
}

function handleClick(event) {
  if (mouseDown.value == false) return;

  const rect = canvas.value!.getBoundingClientRect() // canvas's position on screen - as clientXY are abosolute coordinates
  const x = Math.floor((event.clientX - rect.left) / CELL_SIZE)
  const y = Math.floor((event.clientY - rect.top) / CELL_SIZE)
  drawPixel(x, y, color.value)
  console.log(event.clientX)
}
function mDown(event) {
  mouseDown.value = true
  handleClick(event)
}
function mUp(event) {
  mouseDown.value = false
}
function colorPick(c: string)
{
  color.value = c

  // sound effect
  const audio = new Audio("/assets/pop.mp3");
  audio.play();
}
function clearCanvas() {
  //ctx.clearRect(0, 0, 800, 600)
  grid.value = new Array(80 * 60).fill("white");
  loadCanvas();
  localStorage.removeItem('grid');

  // sound effect
  const audio = new Audio("/assets/clear.mp3");
  audio.play();
}
function mouseEnterColorButtons(c) {
  hovering.value = c
}
function saveCanvas() {
  const link = document.createElement('a')
  link.download = 'drawing.png'
  link.href = canvas.value!.toDataURL()
  link.click()
}
</script>

<template>
  <canvas ref="canvas" 
  @mousedown="mDown" @mouseup="mUp" @mouseleave="mUp"
  @mousemove="handleClick" @click="handleClick"
  @contextmenu.prevent/>

  <div id="bottom-bar">
    <div id="color-buttons">
      <div v-for="items in colors" :key="items.color" :id="items.color" @click="colorPick(items.color)"
      :style="{backgroundColor: (hovering === items.color || color === items.color) ? items.hover : items.color}"
      @mouseenter="mouseEnterColorButtons(items.color)" @mouseleave="hovering = null"></div>
    </div>
    <div id="clear-save"> 
      <button id="save" @click="saveCanvas">Save</button>
      <button id="clear" @click="clearCanvas">Clear</button>
    </div>
  </div>
</template>

<style lang="scss">
@use './styles/app.scss';

button {
  background-color: white;
  color: blue;
  &:hover {
    background-color: cyan;
  }  
  &:active {
    background-color: white;
  }
}
</style>