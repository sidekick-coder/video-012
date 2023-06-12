<script setup>
import { ref, computed } from 'vue'

const show = ref(false)
const activatorRef = ref(null)
const position = ref({
  x: 0,
  y: 0
})

const style = computed(() => ({
  top: `${position.value.y}px`,
  left: `${position.value.x}px`
}))

function onRef(element) {
  activatorRef.value = element
}

function onMouseenter(event) {
  let x = event.clientX
  let y = event.clientY

  const [rects] = activatorRef.value?.getClientRects() ?? []

  if (rects) {
    x = rects.x
    y = rects.y + rects.height
  }

  position.value.x = x
  position.value.y = y

  show.value = true
}

function onMouseleave() {
  show.value = false
}
</script>
<template>
  <slot
    name="activator"
    :attrs="{
      ref: onRef,
      onMouseenter,
      onMouseleave
    }"
  />

  <Teleport to="body">
    <transition
      enter-active-class="transition duration-200"
      leave-active-class="transition duration-200"
      enter-from-class="opacity-0 translate-y-2"
      leave-to-class="opacity-0 translate-y-2"
    >
      <div
        v-if="show"
        class="fixed rounded bg-zinc-900 px-4 py-2 text-sm text-white"
        :style="style"
      >
        <slot />
      </div>
    </transition>
  </Teleport>
</template>
