<template>
  
</template>

<script>
import { PerspectiveCamera, Vector3 } from 'three';
import Vue from 'vue';

export default {
  name: 'perspective-camera',
  props: {
    fov: {
      type: Number,
      default: 75
    },
    aspect: {
      type: Number,
      default: 0
    },
    near: {
      type: Number,
      default: 0.1
    },
    far: {
      type: Number,
      default: 1000
    },
    position: {
      type: Vector3,
      default: () => new Vector3(0, 0, 5)
    }
  },
  data() {
    return {
      camera: null
    }
  },
  methods: {
    reposition() {
      this.camera.position.copy(this.position);
    }
  },
  mounted() {
    this.camera = new PerspectiveCamera(this.fov, this.aspect || window.innerWidth / window.innerHeight, this.near, this.far);
    this.reposition();
  }
}
</script>