<template>
  <div id="app">
    <image-carousel />
  </div>
</template>

<script>
import ImageCarousel from './components/ImageCarousel';

export default {
  name: 'App',
  components: {
    ImageCarousel,
  },
};
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>
