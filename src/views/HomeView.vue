<template>
  <div class="home">
    <div class="container">
      <h1>AppButton - с темами light/dark</h1>

      <!-- Обычные кнопки с разными темами -->
      <div class="section">
        <h2>Обычные кнопки</h2>
        <div class="button-group">
          <AppButton text="Dark тема" theme="dark" />
          <AppButton text="Light тема" theme="light" />
        </div>
        <div class="button-group">
          <AppButton text="Dark (small)" size="small" theme="dark" />
          <AppButton text="Light (small)" size="small" theme="light" />
        </div>
        <div class="button-group">
          <AppButton text="Dark (large)" size="large" theme="dark" />
          <AppButton text="Light (large)" size="large" theme="light" />
        </div>
      </div>

      <!-- Outlined кнопки с $secondary-4 бордером -->
      <div class="section">
        <h2>Outlined кнопки (бордер $secondary-4)</h2>
        <div class="button-group">
          <AppButton text="Dark outlined" theme="dark" outlined />
          <AppButton text="Light outlined" theme="light" outlined />
        </div>
        <div class="button-group">
          <AppButton text="Small" size="small" theme="dark" outlined />
          <AppButton text="Large" size="large" theme="light" outlined />
        </div>
      </div>

      <!-- Круглые кнопки с темами -->
      <div class="section">
        <h2>Круглые кнопки</h2>
        <div class="button-group">
          <AppButton size="small" :icon-left="ArrowUpRightIcon" theme="dark" />
          <AppButton size="small" :icon-left="SearchIcon" theme="light" />
          <AppButton size="medium" :icon-left="SearchIcon" theme="dark" />
          <AppButton size="medium" :icon-left="SearchIcon" theme="light" />
          <AppButton size="large" :icon-left="SearchIcon" theme="dark" />
          <AppButton size="large" :icon-left="SearchIcon" theme="light" />
        </div>
        <div class="button-group">
          <AppButton size="small" :icon-left="SearchIcon" theme="dark" outlined />
          <AppButton size="small" :icon-left="SearchIcon" theme="light" outlined />
          <AppButton size="medium" :icon-left="SearchIcon" theme="dark" outlined />
          <AppButton size="medium" :icon-left="SearchIcon" theme="light" outlined />
        </div>
      </div>

      <!-- Кнопки с иконкой и текстом -->
      <div class="section">
        <h2>Кнопки с иконкой и текстом</h2>
        <div class="button-group">
          <AppButton
            text="Поиск"
            theme="dark"
            :icon-left="ArrowUpRightIcon"
          />
          <AppButton
            text="Поиск"
            theme="light"
            :icon-left="SearchIcon"
          />
          <AppButton
            text="Далее"
            theme="dark"
            :icon-right="ArrowIcon"
          />
          <AppButton
            text="Далее"
            theme="light"
            :icon-right="ArrowIcon"
          />
        </div>
      </div>

      <!-- Кастомные цвета (переопределяют темы) -->
      <div class="section">
        <h2>Кастомные цвета (переопределяют темы)</h2>
        <div class="button-group">
          <AppButton
            text="Акцентная кнопка"
            theme="dark"
            bg-color="#FAB722"
            text-color="#232422"
          />
          <AppButton
            text="Кастомная обводка"
            theme="dark"
            outlined
            border-color="#FAB722"
            text-color="#FAB722"
          />
        </div>
      </div>

      <!-- Отключенные кнопки -->
      <div class="section">
        <h2>Отключенные кнопки</h2>
        <div class="button-group">
          <AppButton text="Dark disabled" theme="dark" disabled />
          <AppButton text="Light disabled" theme="light" disabled />
          <AppButton text="Outlined disabled" theme="dark" outlined disabled />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import AppButton from '@/components/app/AppButton.vue'
import ArrowUpRightIcon from "@/assets/icons/ArrowUpRightIcon.vue";

</script>

<style scoped lang="scss">
.section {
  margin-bottom: 2rem;
  padding: 1.5rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: #fff;
}

.button-group {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
  margin-bottom: 1rem;
  flex-wrap: wrap;
  align-items: center;
}

h2 {
  margin-top: 0;
  margin-bottom: 1rem;
  font-size: 1.25rem;
}
</style>
