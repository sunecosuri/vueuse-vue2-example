<template>
  <div id="app">
    <img src="./logo.svg" />
    <UseDraggable :initialValue="{ x: 10, y: 10 }" v-slot="{ x, y }">
      Drag me! I am at {{x}}, {{y}}
    </UseDraggable>

    <UseDraggable
      v-slot="{ x, y }"
      p="x-4 y-2"
      border="~ gray-400/30 rounded"
      shadow="~ hover:lg"
      class="fixed bg-$vp-c-bg select-none z-24"
      :initial-value="{ x: innerWidth / 3.6, y: 240 }"
      :prevent-default="true"
      :handle="handle"
    >
      <div ref="handle" class="cursor-move">
        👋 Drag here!
      </div>
      <div class="text-xs opacity-50">
        Handle that triggers the drag event
      </div>
      <div class="text-sm opacity-50">
        I am at {{ Math.round(x) }}, {{ Math.round(y) }}
      </div>
    </UseDraggable>
    <br/><br/>
  </div>
</template>

<script lang="ts">
import { ref, defineComponent } from '@vue/composition-api'
import { useCounter, useDraggable } from '@vueuse/core'
import { UseDraggable } from '@vueuse/components'

export default defineComponent({
  components: {
    UseDraggable,
  },
  setup() {
    const el = ref<HTMLElement | null>(null)
    const { count, inc, dec } = useCounter()
    const innerWidth = window.innerWidth
    const { x, y, style } = useDraggable(el, {
      initialValue: { x: innerWidth / 4.2, y: 80 },
      preventDefault: true,
    })

    return {
      x, 
      y,
      style,
      innerWidth,
      count,
      inc,
      dec,
    }
  }
})
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Noto+Serif&display=swap');

html, body, h1, h2, h3, p {
  font-family: 'Noto Serif', serif;
  user-select: none;
}

#app {
  text-align: center;
  color: rgba(0,0,0,0.4);
}
img {
  width: 500px;
}
a {
  color: #41b883;
  text-decoration: none;
  cursor: pointer;
}
</style>
