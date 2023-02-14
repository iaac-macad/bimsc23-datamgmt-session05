<template>
  <div id="viewport" class="flex flex-col p-4">
    <p>{{ size }}</p>
    <div id="threejs-container" class="py-5"></div>
  </div>


</template>

<script setup>
// Imports;
import { ref, onMounted } from 'vue'
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
import { store } from '@/store'

const props = defineProps(['val'])

const size = ref(store.count)

// BOILERPLATE //
let scene, camera, renderer, controls
let width = 500;
let heigh = 700;

store.count = 10

// add fun shape
const geometry = new THREE.TorusKnotGeometry(store.count, 3, 200, 16);
const material = new THREE.MeshNormalMaterial();

function init() {
  
    // create a scene and a camera
    scene = new THREE.Scene()
    scene.background = new THREE.Color(1, 1, 1)
    camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
    camera.position.z = - 30

    // create the renderer and add it to the html
    renderer = new THREE.WebGLRenderer({ antialias: true })
    renderer.setSize(width, heigh);
    document.getElementById("threejs-container").appendChild(renderer.domElement);

    // add some controls to orbit the camera
    controls = new OrbitControls(camera, renderer.domElement)

    // add a directional light
    const directionalLight = new THREE.DirectionalLight(0xffffff)
    directionalLight.intensity = 2
    scene.add(directionalLight)

    const ambientLight = new THREE.AmbientLight()
    scene.add(ambientLight)
    


    const shape = new THREE.Mesh(geometry, material);
    scene.add(shape);
}

function animate() {
    requestAnimationFrame(animate)
    controls.update();
    renderer.render(scene, camera)
}


function updateTorus()
{

}

onMounted(() => {
  init();
  animate()

})


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
}
</style>