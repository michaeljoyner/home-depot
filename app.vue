<template>
  <div class="min-h-screen min-w-screen pt-24">
    <ClientOnly>
      <div class="mt-24 max-w-lg mx-auto bg-white shadow flex flex-col gap-6 items-center p-6 rounded-lg">
        <p class="font-black text-lg text-center">Hello Mr. Pi</p>

        <div class="flex gap-6 justify-center">
          <div>
            <button @click="pushButton('yellow')" type="button" class="w-24 h-24 rounded-full bg-yellow-400"></button>
          </div>
          <div>
            <button @click="pushButton('green')" type="button" class="w-24 h-24 rounded-full bg-emerald-400"></button>
          </div>

          <div>
            <button @click="pushButton('red')" type="button" class="w-24 h-24 rounded-full bg-red-400"></button>
          </div>
        </div>
        <div>
          <pre>{{ error }}</pre>
        </div>
      </div>
    </ClientOnly>
  </div>
</template>

<script setup>
const error = ref("foo");
const pushButton = (name) => {
  $fetch("https://raspberrypi.local/buttons", {
    body: { key: "1", name },
    method: "POST",
  })
    .catch((err) => (error.value = err.data))
    .finally((d) => (error.value = d));
};
</script>
