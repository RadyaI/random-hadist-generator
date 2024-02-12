<!-- Star.vue -->
<template>
    <div class="star" :style="{ top: `${position.y}px`, left: `${position.x}px` }"></div>
</template>
  
<script>
export default {
    name: 'app',
    props: ['position'],
};
</script>
  
<style scoped>
.star {
    width: 2px;
    height: 2px;
    background-color: #fff;
    position: absolute;
    animation: fall linear infinite;
}

@keyframes fall {
    to {
        transform: translateY(100vh);
    }
}
</style>
  