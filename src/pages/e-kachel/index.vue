<script setup lang="ts">

</script>

<template>
  <div class="w-full">
    <div class="flex flex-col">
      <div flex>
        <p class="mx-105">
          dringend
        </p>
        <p class="ml-36">
          verzichtbar
        </p>
      </div>
      <div class="flex mb-6">
        <p class=" w-36">
          wichtig
        </p>
        <div class="w-150 h-150 mx-5 rounded-2xl bg-red-400">
          A Aufgaben
        </div>
        <div class="w-150 h-150 mx-5 rounded-2xl  bg-red-400">
          B Aufgaben
        </div>
      </div>
      <div class="flex mt-6">
        <p class="  w-36">
          nichtig
        </p>
        <div class="w-150 h-150 mx-5 rounded-2xl  bg-red-400">
          C Aufgaben
        </div>
        <div class="w-150 h-150 mx-5 rounded-2xl  bg-red-400">
          D Aufgaben
        </div>
      </div>
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: home
</route>
