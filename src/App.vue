<template>
  <div id="app">
      <main class="bg-gray-200">
        <div class="py-10 px-10 grid grid-cols-4 gap-10 md:min-h-screen">
          <LeftSide  class="col-span-4 md:col-span-1" />
          <RightSide class="col-span-4 md:col-span-3" />
        </div>
      </main>
  </div>
</template>

<script>
import LeftSide from './components/LeftSide.vue'
import RightSide from './components/RightSide.vue' 
export default {
  name: 'App',
  components: {
    LeftSide,
    RightSide
  }
}
</script>
