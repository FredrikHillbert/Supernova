<template>
     
   <div class="container">
        <iframe class="responsive-iframe"  src='https://mars.nasa.gov/layout/embed/image/mslweather/'  scrolling='yes' frameborder='0' allowfullscreen = true></iframe>
    </div>
  
</template>

<script>
export default {

}
</script>

<style>

.container {
  position: relative;
  width: 100%;
  height: 100%;
  padding-top: 56.25%; /* 16:9 Aspect Ratio (divide 9 by 16 = 0.5625) */
}

.container {
  padding-top: 150%; /* 4:3 Aspect Ratio */
}



/* Then style the iframe to fit in the container div with full height and width */
.responsive-iframe {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100%;
}

</style>