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
const props = defineProps(['radiusTop', 'radiusBottom', 'height', 'radialSegments', 'openEnded']);

// Three js objects
let renderer, camera, scene, controls, geometry;

let width = 1000;
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
  scene.background = new THREE.Color("#666666");

  // orbit controls
  controls = new OrbitControls(camera, renderer.domElement);

  // add fun shape
  createCylinder(5, 5, 5, 32);
  animate();
}

// for controls update
function animate() {
  requestAnimationFrame(animate);
  controls.update();
  renderer.render(scene, camera);
}

function createCylinder(radiusTop, radiusBottom, height, radialSegments,openEnded) {
  geometry = new THREE.CylinderGeometry(radiusTop, radiusBottom, height, radialSegments);
  const material = new THREE.MeshNormalMaterial();
  const cylinder = new THREE.Mesh(geometry, material)
  scene.add(cylinder);
}

function onSliderChange(color) {
  scene.clear();
  createCylinder(props.radiusTop, props.radiusBottom, props.height, props.radialSegments);

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
  border-width: 1px;
  border-radius: 3px;
  margin: 12px;
  height: 1000px;
  width: 1000px;
  min-width: 200px;
  position: inherit;
}
</style>