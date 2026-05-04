<template>
  <button
    class="app-button"
    :class="[
      `app-button--${size}`,
      `app-button--${theme}`,
      {
        'app-button--outlined': outlined,
        'app-button--circle': isCircle
      }
    ]"
    :style="buttonStyles"
    :disabled="disabled"
    @click="handleClick"
  >
    <span v-if="iconLeft" class="app-button__icon app-button__icon--left">
      <component :is="getIconComponent(iconLeft)" />
    </span>

    <span v-if="hasText" class="app-button__text">
      <slot>{{ text }}</slot>
    </span>

    <span v-if="iconRight" class="app-button__icon app-button__icon--right">
      <component :is="getIconComponent(iconRight)" />
    </span>
  </button>
</template>

<script setup>
import { computed } from 'vue'
import { useSlots } from 'vue'

const props = defineProps({
  text: {
    type: String,
    default: ''
  },
  size: {
    type: String,
    default: 'medium',
    validator: (value) => ['small', 'medium', 'large'].includes(value)
  },
  theme: {
    type: String,
    default: 'dark',
    validator: (value) => ['light', 'dark'].includes(value)
  },
  outlined: {
    type: Boolean,
    default: false
  },
  disabled: {
    type: Boolean,
    default: false
  },
  type: {
    type: String,
    default: 'button'
  },
  iconLeft: {
    type: [Object, String], // Может быть как компонент, так и строка с названием
    default: null
  },
  iconRight: {
    type: [Object, String],
    default: null
  },
  bgColor: {
    type: String,
    default: null
  },
  textColor: {
    type: String,
    default: null
  },
  borderColor: {
    type: String,
    default: null
  }
})

const emit = defineEmits(['click'])

// Карта высот для разных размеров
const heightMap = {
  small: 40,
  medium: 48,
  large: 56
}

// Карта отступов
const paddingMap = {
  small: { default: 20, iconOnly: 10 },
  medium: { default: 24, iconOnly: 12 },
  large: { default: 28, iconOnly: 14 }
}

// Регистрируем доступные иконки (можно импортировать и использовать динамически)
const iconComponents = import.meta.glob('@/components/icons/*.vue', { eager: true })

// Функция для получения компонента иконки
const getIconComponent = (icon) => {
  if (typeof icon === 'string') {
    // Если передана строка, ищем компонент по имени
    const componentName = `Icon${icon.charAt(0).toUpperCase() + icon.slice(1)}`
    const iconPath = Object.keys(iconComponents).find(path =>
      path.includes(`/${componentName}.vue`)
    )
    if (iconPath) {
      return iconComponents[iconPath].default
    }
    console.warn(`Icon "${icon}" not found`)
    return null
  }
  // Если передан объект/компонент, возвращаем как есть
  return icon
}

// Проверяем, есть ли текст
const hasText = computed(() => {
  return props.text || !!useSlots().default
})

// Проверяем, круглая ли кнопка
const isCircle = computed(() => {
  return !hasText.value && (props.iconLeft || props.iconRight)
})

// Вычисляем скругление
const borderRadius = computed(() => {
  if (isCircle.value) return '50%'
  return `${heightMap[props.size] / 2}px`
})

// Вычисляем отступы
const padding = computed(() => {
  if (isCircle.value) {
    return `${paddingMap[props.size].iconOnly}px`
  }

  const hasIcon = props.iconLeft || props.iconRight
  if (hasIcon && hasText.value) {
    return `0 ${paddingMap[props.size].default - 4}px`
  }

  const paddingValue = hasIcon && !hasText.value
    ? paddingMap[props.size].iconOnly
    : paddingMap[props.size].default

  return `0 ${paddingValue}px`
})

// Ширина для круглой кнопки
const circleWidth = computed(() => {
  if (isCircle.value) return `${heightMap[props.size]}px`
  return 'auto'
})

// Динамические стили
const buttonStyles = computed(() => {
  const styles = {
    borderRadius: borderRadius.value,
    padding: padding.value,
    width: circleWidth.value
  }

  if (props.bgColor && !props.outlined) {
    styles.backgroundColor = props.bgColor
  }

  if (props.textColor) {
    styles.color = props.textColor
  }

  if (props.outlined && props.borderColor) {
    styles.borderColor = props.borderColor
  }

  return styles
})

const handleClick = (event) => {
  if (!props.disabled) {
    emit('click', event)
  }
}
</script>

<style scoped lang="scss">
@use '@/assets/scss/index.scss' as *;

.app-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  border: none;
  cursor: pointer;
  font-family: $font-family-primary;
  font-weight: $font-weight-medium;
  transition: all 0.3s ease;
  white-space: nowrap;

  &--small {
    height: 40px;
    font-size: $font-size-p3;
    line-height: $line-height-p3;
  }

  &--medium {
    height: 48px;
    font-size: $font-size-p2;
    line-height: $line-height-p2;
  }

  &--large {
    height: 56px;
    font-size: $font-size-p2;
    line-height: $line-height-p2;
  }

  &:not(&--outlined) {
    &.app-button--dark {
      background-color: $primary-1;
      color: $secondary-4;

      &:hover:not(:disabled) {
        background-color: $primary-3;
        transform: translateY(-1px);
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
      }
    }

    &.app-button--light {
      background-color: $primary-3;
      color: $secondary-4;

      &:hover:not(:disabled) {
        background-color: $primary-1;
        transform: translateY(-1px);
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
      }
    }

    &:active:not(:disabled) {
      transform: translateY(0);
    }
  }

  &--outlined {
    background-color: transparent;
    border: 2px solid $secondary-4;
    color: $secondary-4;

    &.app-button--dark {
      &:hover:not(:disabled) {
        background-color: $primary-1;
        border-color: $primary-1;
        transform: translateY(-1px);
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
      }
    }

    &.app-button--light {
      &:hover:not(:disabled) {
        background-color: $primary-3;
        border-color: $primary-3;
        transform: translateY(-1px);
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
      }
    }

    &:active:not(:disabled) {
      transform: translateY(0);
    }
  }

  &--circle {
    padding: 0 !important;
    aspect-ratio: 1 / 1;

    .app-button__text {
      display: none;
    }
  }

  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
    transform: none !important;
  }

  &__icon {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 20px;
    height: 20px;
    flex-shrink: 0;

    svg {
      width: 100%;
      height: 100%;
    }
  }

  &__text {
    display: inline-block;
  }
}
</style>
