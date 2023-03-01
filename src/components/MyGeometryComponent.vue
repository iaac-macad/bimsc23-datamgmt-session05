<template>
    <div>
      <select :value="selectedMaterial" @change="$emit('update:selectedMaterial', $event.target.value)">
        <option v-for="(material, index) in materials" :key="index" :value="material.name">{{ material.name }}</option>
      </select>
    </div>
  </template>
  
  <script>
  import * as THREE from 'three';
  
  export default {
    props: {
      geometry: {
        type: THREE.Geometry,
        required: true
      },
      selectedMaterial: {
        type: String,
        required: true
      }
    },
    data() {
      return {
        materials: [
          { name: 'Basic', material: new THREE.MeshBasicMaterial({ color: 0xff0000 }) },
          { name: 'Lambert', material: new THREE.MeshLambertMaterial({ color: 0xff0000 }) },
          { name: 'Phong', material: new THREE.MeshPhongMaterial({ color: 0xff0000 }) },
        ],
      };
    },
    watch: {
      selectedMaterial() {
        this.setMaterial();
      }
    },
    mounted() {
      this.setMaterial();
    },
    methods: {
      setMaterial() {
        const selected = this.materials.find(m => m.name === this.selectedMaterial);
        if (selected) {
          this.geometry.material = selected.material;
        }
      }
    }
  };
  </script>
  