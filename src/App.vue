<script setup>
import { ref, onMounted } from 'vue';

const isVisible = ref(false);

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true;
  }, 300); // Adjust delay as needed
});


</script>

<template>
<header class="bg-slate-950 text-white p-4 ">
  <nav class="flex justify-between items-center">
    <h1 class="text-3xl font-bold text-color-slate-950  my-5100">SHIEN FACTORY</h1>
    <ul class="flex space-x-4">
      <li><a href="#home" class="hover:bg-slate-50 rounded px-5 py-5 hover:text-slate-950 hover:transition duration-500">Home</a></li>
      <li><a href="#about" class="hover:bg-lime-500 rounded px-5 py-5 hover:text-white hover:transition duration-500">About</a></li>
      <li><a href="#projects" class="hover:bg-violet-900 rounded px-5 py-5 hover:text-white hover:transition duration-500">Projects</a></li>
      <li><a href="#contact" class="hover:bg-fuchsia-500 rounded px-5 py-5 hover:text-white hover:transition duration-500">Contact</a></li>
    </ul>
  </nav>
</header>

<section id="home" class="bg-cover bg-center h-screen"  style="background-image: url('public\image\purple.jpg');">
    <div class="flex items-center justify-center h-full bg-black bg-opacity-50">
      <div class="text-center ">
        <div :class="{'opacity-0': !isVisible, 'opacity-100': isVisible}" class="transition-opacity duration-1000 ease-in-out">
          <img src="/image/halfbod.jpg" alt="my glorious blue eyed king" class="circle rotate ">
          <h2 class="text-4xl font-bold mb-4 text-white">Hi, I'm Firhan</h2>
          <div class="animate-pulse">
            <p class="text-2xl mb-8 text-white">A on-the-lifeline-KICT-Student.</p>
          </div>
        </div>
      </div>
    </div>
  </section>




</template>

<style >
body{
  @apply bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500
}
body{
  font-family: 'General Sans', sans-serif;
}
.circle {
  width: 250px; /* Adjust size to preference */
  height: 250px;
  border-radius: 50%;
  border: 4px solid #000; /* Customize border width and color */
  object-fit: cover; /* Ensures the image covers the element */
  margin-bottom: 30px;
  margin-left: 45px;
}
.rotate {
  animation: rotate360 10s linear infinite;
}

@keyframes rotate360 {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
