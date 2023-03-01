<template>
  <div id="viewport" class="flex flex-col p-4">
    <div id="threejs-container" class="py-5"></div>
  </div>
</template>

<script setup>
// Imports;
import { onMounted, onUpdated } from "vue";
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";

// Property coming from parent component
const props = defineProps(["size"]);

// Three js objects
let renderer, camera, scene, controls, geometry;

let width = 600;
let heigh = 700;

function init() {
  // rendeder
  renderer = new THREE.WebGLRenderer();
  renderer.setSize(width, heigh);
  renderer.setPixelRatio(window.devicePixelRatio);
  document.getElementById("threejs-container").appendChild(renderer.domElement);

  // camera
  camera = new THREE.PerspectiveCamera(75, width / heigh, 0.1, 1000);
  camera.position.set(0, 0, 40);

  // scene
  scene = new THREE.Scene();
  scene.background = new THREE.Color("white");

  // orbit controls
  controls = new OrbitControls(camera, renderer.domElement);

  // add fun shape
  createBox(25, 25, 25);
  animate();
}

// for controls update
function animate() {
  requestAnimationFrame(animate);
  controls.update();
  renderer.render(scene, camera);
}

function createBox(l, w, h,) {
  geometry = new THREE.BoxGeometry(l, w, h);
  const material = new THREE.MeshNormalMaterial({color: '#8AC'});;
  const sphere = new THREE.Mesh(geometry, material);
  scene.add(sphere);
}

function onSliderChange(color) {
  scene.clear();
  createBox(props.size, props.size, props.size);
}

// This function runs at the beginning of the component lifecycle.
// More about Vue lifecycles: https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram
onMounted(() => {
  init();
  animate();
});

// This function runs when DOM updates.
onUpdated(() => {
  // text content should be the same as current `count.value`
  onSliderChange();
});
</script>

<style scoped>
#viewport {
  border-style: dashed;
  border-color: #d2dfe8;
  border-width: 4px;
  border-radius: 10px;
  margin: 12px;
  height: calc(100vh - 105px);
  width: 600px;
  min-width: 200px;
  position: relative;
}
</style>