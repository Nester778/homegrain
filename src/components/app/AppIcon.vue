<template>
  <component
    :is="icon"
    class="app-icon"
    :style="iconStyles"
  />
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  icon: {
    type: Object,
    required: true
  },
  size: {
    type: [String, Number],
    default: null
  },
  color: {
    type: String,
    default: null
  }
})

const iconStyles = computed(() => {
  const styles = {}

  if (props.size) {
    const sizeValue = typeof props.size === 'number' ? `${props.size}px` : props.size
    styles.width = sizeValue
    styles.height = sizeValue
  }

  if (props.color) {
    styles.color = props.color
  }

  return styles
})
</script>

<style scoped>
.app-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  width: 24px;
  height: 24px;
}

.app-icon svg {
  width: 100%;
  height: 100%;
}
</style>
