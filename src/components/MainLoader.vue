<template>
    <!-- Credits: https://css-loaders.com/ -->
    <div class="loader"></div>
</template>

<style scoped>
/* Credits: https://css-loaders.com/ */
/* HTML: <div class="loader"></div> */
.loader {
    width: 20px;
    aspect-ratio: 1;
    background: #25b09b;
    box-shadow: 0 0 60px 15px #25b09b;
    transform: translate(-80px);
    clip-path: inset(0);
    animation:
        l4-1 0.5s ease-in-out infinite alternate,
        l4-2 1s   ease-in-out infinite;

    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
@keyframes l4-1 {
  100% {transform: translateX(80px)}
}
@keyframes l4-2 {
   33% {clip-path: inset(0 0 0 -100px)}
   50% {clip-path: inset(0 0 0 0)     }
   83% {clip-path: inset(0 -100px 0 0)}
}
</style>