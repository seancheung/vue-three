<template>
  <div>
    <slot name="object"></slot>
  </div>
</template>

<script>
import { Scene } from 'three';
import Vue from 'vue';

export default {
  name: 'scene',
  props: {
    objects: Array
  },
  data() {
    return {
      scene: null
    }
  },
  mounted() {
    this.scene = new Scene();
    if (this.$slots.object && this.$slots.object.length) {
      for (let i = 0; i < this.$slots.object.length; i++) {
        this.scene.add(this.$slots.object[i].componentInstance.object);
      }
    }
    if (this.objects && this.objects.length) {
      for (let i = 0; i < this.objects.length; i++) {
        this.scene.add(this.objects[i]);
      }
    }
  }
}
</script>