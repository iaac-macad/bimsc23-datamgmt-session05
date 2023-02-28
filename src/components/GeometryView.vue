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
const props = defineProps(["radius", "height", "radialSegments"]);

// Three js objects
let renderer, camera, scene, controls, geometry;

let width = 1200;
let heigh = 800;

function init() {
  // rendeder
  renderer = new THREE.WebGLRenderer();
  renderer.setSize(width, heigh);
  renderer.setPixelRatio(window.devicePixelRatio);
  document.getElementById("threejs-container").appendChild(renderer.domElement);

  // camera
  camera = new THREE.PerspectiveCamera(70, width / heigh, 0.1, 1000);
  camera.position.set(30, 30, 20);

  // scene
  scene = new THREE.Scene();
  scene.background = new THREE.Color("lightblue");

  // orbit controls
  controls = new OrbitControls(camera, renderer.domElement);

  // add fun shape
  createCone(20, 25, 10);
  animate();
}

// for controls update
function animate() {
  requestAnimationFrame(animate);
  controls.update();
  renderer.render(scene, camera);
}

function createCone(radius, height, radialSegments) {
  geometry = new THREE.ConeGeometry(radius, height, radialSegments);
  const material = new THREE.MeshNormalMaterial();
  const sphere = new THREE.Mesh(geometry, material);
  scene.add(sphere);
}

function onSliderChange() {
  scene.clear();
  createCone(props.radius, props.height, props.radialSegments);
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
  height: 800px;
  width: 1200px;
  min-width: 200px;
  position: inherit;
}
</style>