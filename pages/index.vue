<template>
  <div>
    <AppBar />
  </div>
</template>

<script>
import { thisTypeAnnotation } from '@babel/types';
import { longStackSupport } from 'q';
import AppBar from '../components/AppBar.vue';
export default {
    name: "Index",
    components: { AppBar },
    
}
</script>