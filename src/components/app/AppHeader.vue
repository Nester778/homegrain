<template>
  <header class="app-header">
    <nav class="nav-container">
      <div class="logo">
        <h3 class="color-primary-3">logo</h3>
      </div>

      <button
        class="burger-menu"
        :class="{ 'burger-menu--active': isMenuOpen }"
        @click="toggleMenu"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>

      <div
        class="mobile-overlay"
        v-if="isMenuOpen"
        @click="closeMenu"
      ></div>

      <ul
        class="nav-links"
        :class="{ 'nav-links--open': isMenuOpen }"
      >
        <li @click="closeMenu">
          <router-link to="/">
            <h5>Головна сторінка</h5>
          </router-link>
        </li>
        <li @click="closeMenu">
          <router-link to="/catalog">
            <h5>Каталог</h5>
          </router-link>
        </li>
        <li @click="closeMenu">
          <router-link to="/custom">
            <h5>Роботи під замовлення</h5>
          </router-link>
        </li>
        <li @click="closeMenu">
          <router-link to="/contacts">
            <h5>Контакти</h5>
          </router-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script setup>
import { ref, watch } from 'vue'

const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

watch(isMenuOpen, (newValue) => {
  if (newValue) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
  }
})
</script>

<style scoped lang="scss">
@use '@/assets/scss/index.scss' as *;

.app-header {
  padding: 1rem;
  background-color: $background;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  position: relative;
  z-index: 1000;
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

.logo {
  flex-shrink: 0;

  h3 {
    margin: 0;
  }
}

.burger-menu {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 21px;
  background: transparent;
  border: none;
  cursor: pointer;
  z-index: 100;
  position: relative;

  span {
    width: 100%;
    height: 3px;
    background-color: $primary-1;
    border-radius: 2px;
    transition: all 0.3s ease;
  }

  &--active {
    span:first-child {
      transform: translateY(9px) rotate(45deg);
    }

    span:nth-child(2) {
      opacity: 0;
    }

    span:last-child {
      transform: translateY(-9px) rotate(-45deg);
    }
  }
}

.mobile-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 90;
}

.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
  margin: 0;

  a {
    color: $text-primary;
    text-decoration: none;
    transition: color 0.3s ease;

    &:hover {
      color: $primary-3;
    }

    h5 {
      margin: 0;
    }
  }
}

@media (max-width: 768px) {
  .burger-menu {
    display: flex;
  }

  .nav-links {
    position: fixed;
    top: 0;
    right: -100%;
    width: 80%;
    max-width: 320px;
    height: 100vh;
    background-color: $background;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 2rem;
    margin: 0;
    padding: 2rem;
    transition: right 0.3s ease;
    z-index: 95;

    &--open {
      right: 0;
    }

    li {
      width: 100%;
      text-align: center;
    }

    a {
      display: block;
      padding: 0.75rem;
      font-size: 1.125rem;
    }
  }
}

@media (min-width: 769px) {
  .nav-links {
    position: static !important;
    width: auto !important;
    height: auto !important;
    flex-direction: row !important;
    justify-content: flex-end !important;
    background: none !important;
    padding: 0 !important;

    &--open {
      right: auto !important;
    }
  }

  .mobile-overlay {
    display: none;
  }
}
</style>
