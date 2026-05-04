<template>
  <footer>
    <div class="container">
      <div class="footer">
        <!-- Контактная информация -->
        <div class="footer-section">
          <h4>Контактна інформація</h4>
          <div class="footer-content">
            <div class="footer-content-item">
              <AppIcon :icon="PhoneIcon" />
              <p>тел. +38 (011) 11-11-111</p>
            </div>
            <div class="footer-content-item">
              <AppIcon :icon="MailIcon" />
              <p>mail@gmail.com</p>
            </div>
            <div class="footer-content-item">
              <AppIcon :icon="GeoTagIcon" />
              <p>м. Харків</p>
            </div>
          </div>
        </div>

        <!-- Меню -->
        <div class="footer-section">
          <h4>Меню</h4>
          <div class="footer-content">
            <div class="footer-content-item">
              <router-link to="/"><p>Головна сторінка</p></router-link>
            </div>
            <div class="footer-content-item">
              <router-link to="/catalog"><p>Каталог</p></router-link>
            </div>
            <div class="footer-content-item">
              <router-link to="/custom"><p>Роботи під замовлення</p></router-link>
            </div>
            <div class="footer-content-item">
              <router-link to="/contacts"><p>Контакти</p></router-link>
            </div>
          </div>
        </div>

        <!-- Продукция -->
        <div class="footer-section footer-section--products">
          <h4>Продукція</h4>
          <div class="footer-content footer-content--grid">
            <div class="footer-content-item">
              <router-link to="/catalog"><p>Дерев'яні стінові панелі</p></router-link>
            </div>
            <div class="footer-content-item">
              <router-link to="/catalog"><p>Кавові та журнальні столи</p></router-link>
            </div>
            <div class="footer-content-item">
              <router-link to="/catalog"><p>Крісла</p></router-link>
            </div>
            <div class="footer-content-item">
              <router-link to="/catalog"><p>Міжкімнатні двері</p></router-link>
            </div>
            <div class="footer-content-item">
              <router-link to="/catalog"><p>Обідні столи</p></router-link>
            </div>
            <div class="footer-content-item">
              <router-link to="/catalog"><p>Розкладні стільці</p></router-link>
            </div>
            <div class="footer-content-item">
              <router-link to="/catalog"><p>Стільці комп'ютерні</p></router-link>
            </div>
            <div class="footer-content-item">
              <router-link to="/catalog"><p>Сходи для інтер’єру</p></router-link>
            </div>
          </div>
        </div>

        <div class="footer-section">
          <h4>Додатково</h4>
          <div class="footer-content-icon">
            <AppIcon :icon="WhatsAppIcon" :size="40" />
            <AppIcon :icon="ViberIcon" :size="40" />
            <AppIcon :icon="TelegramIcon" :size="40" />
          </div>
        </div>
      </div>

      <div class="footer-divider"></div>
      <p class="p2 footer-copyright">Copyright &copy; {{ currentYear }}. All Rights Reserved.</p>
    </div>
  </footer>
</template>

<script setup>
import { computed } from 'vue'
import AppIcon from '@/components/app/AppIcon.vue'
import PhoneIcon from '@/assets/icons/PhoneIcon.vue'
import MailIcon from "@/assets/icons/MailIcon.vue"
import GeoTagIcon from "@/assets/icons/GeoTagIcon.vue"
import WhatsAppIcon from "@/assets/icons/WhatsAppIcon.vue"
import ViberIcon from "@/assets/icons/ViberIcon.vue"
import TelegramIcon from "@/assets/icons/TelegramIcon.vue"

const currentYear = computed(() => new Date().getFullYear())
</script>

<style scoped lang="scss">
@use '@/assets/scss/index.scss' as *;

footer {
  background-color: $background-4;
  padding: 48px 0 24px;
  margin-top: auto;
}

.footer {
  display: flex;
  justify-content: space-between;
  gap: 40px;
  margin-bottom: 48px;

  @media (max-width: 1024px) {
    flex-wrap: wrap;
    gap: 32px;
  }
}

.footer-section {
  flex: 1;
  min-width: 160px;

  @media (max-width: 768px) {
    flex: 0 0 calc(50% - 16px);
  }

  @media (max-width: 480px) {
    flex: 0 0 100%;
  }

  &--products {
    flex: 2;

    @media (max-width: 1024px) {
      flex: 1;
      min-width: 250px;
    }
  }
}

.footer-content {
  margin-top: 24px;

  &--grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 0 24px;

    @media (max-width: 768px) {
      grid-template-columns: 1fr;
      gap: 0;
    }
  }
}

.footer-content-item {
  display: flex;
  align-items: center;
  column-gap: 12px;
  margin-top: 16px;

  &:first-child {
    margin-top: 0;
  }

  p {
    margin: 0;
    color: $secondary-3;
    transition: color 0.3s ease;
    white-space: normal;
    word-break: break-word;
  }

  a {
    color: $secondary-3;
    text-decoration: none;
    transition: color 0.3s ease;
    display: inline-block;

    &:hover {
      color: $primary-3;
    }

    p {
      &:hover {
        color: $primary-3;
      }
    }
  }
}

.footer-content-icon {
  display: flex;
  column-gap: 16px;
  margin-top: 24px;
  flex-wrap: wrap;
  gap: 16px;

  .app-icon {
    cursor: pointer;
    transition: transform 0.3s ease, opacity 0.3s ease;

    &:hover {
      transform: translateY(-3px);
      opacity: 0.8;
    }
  }
}

.footer-divider {
  height: 1px;
  width: 100%;
  background: $secondary-3;
  opacity: 0.3;
}

.footer-copyright {
  margin-top: 24px;
  color: $secondary-3;
}

// Дополнительные адаптивные настройки
@media (max-width: 768px) {
  footer {
    padding: 40px 0 20px;
  }

  .footer {
    margin-bottom: 32px;
    gap: 32px;
  }

  .footer-content-item {
    margin-top: 12px;
  }

  .footer-content-icon {
    margin-top: 20px;
  }
}

@media (max-width: 480px) {
  footer {
    padding: 32px 0 16px;
  }

  .footer {
    margin-bottom: 24px;
    gap: 28px;
  }

  h4 {
    font-size: 18px;
    margin-bottom: 16px;
  }

  .footer-content-item {
    margin-top: 10px;

    p {
      font-size: 14px;
    }
  }

  .footer-content-icon {
    .app-icon {
      width: 32px !important;
      height: 32px !important;
    }
  }
}

// Для очень больших экранов
@media (min-width: 1440px) {
  .footer {
    gap: 80px;
  }
}
</style>
