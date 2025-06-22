<template>
  <header ref="headerRef">
    <div class="pizza__logo">
      <a href="/">
        <img :src="logo" alt="logo" priority width="215" height="38" />
      </a>
    </div>

    <!-- Hamburger Menu Button -->
    <button
      class="pizza__hamburger"
      @click="isMenuOpen = !isMenuOpen"
      :class="{ 'is-active': isMenuOpen }"
    >
      <span></span>
      <span></span>
      <span></span>
    </button>

    <!-- Navigation Menu -->
    <nav class="pizza__nav" :class="{ 'is-open': isMenuOpen }">
      <a href="#" class="pizza__nav-link">Home</a>
      <a href="#" class="pizza__nav-link pizza__nav-link--active">Order</a>
      <a href="#" class="pizza__nav-link">About</a>
      <a href="#" class="pizza__nav-link">Blog</a>
      <a href="#" class="pizza__nav-link">Contact us</a>
    </nav>

    <div class="pizza__auth" :class="{ 'is-open': isMenuOpen }">
      <button class="pizza__auth-login">Login</button>
      <button class="pizza__auth-register">Register</button>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted } from "vue";
import logo from "/assets/img/logo.svg";

const headerRef = ref(null);
const headerHeight = ref(0);
const isMenuOpen = ref(false);

onMounted(() => {
  if (headerRef.value) {
    headerHeight.value = headerRef.value.offsetHeight;
    // Set the margin-bottom to the negative header height
    headerRef.value.style.marginBottom = `-${headerHeight.value}px`;
  }
});
</script>

<style lang="scss" scoped>
@use "@/assets/scss/variables.scss" as *;
@use "@/assets/scss/mixins.scss" as *;

header {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1.5rem 0;
  z-index: 99;
  position: relative;
  & {
    @include container;
  }

  .pizza {
    &__logo {
      & > a {
        display: block;
        width: 9.5em;
        img {
          width: 100%;
          height: 100%;
          vertical-align: middle;
        }
      }
    }

    &__hamburger {
      display: none;
      background: none;
      border: none;
      cursor: pointer;
      z-index: 100;

      @include responsive(mobile) {
        display: flex;
        flex-direction: column;
        gap: 6px;
      }

      span {
        display: block;
        width: 24px;
        height: 2px;
        background-color: #fff;
        transition: all 0.3s ease;
      }

      &.is-active {
        position: fixed;
        right: 20px;

        span {
          &:first-child {
            transform: translateY(8px) rotate(45deg);
          }
          &:nth-child(2) {
            opacity: 0;
          }
          &:last-child {
            transform: translateY(-8px) rotate(-45deg);
          }
        }
      }
    }

    &__nav {
      display: flex;
      gap: 1.5rem;

      @include responsive(mobile) {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba($primary-color, 0.95);
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 2rem;
        transform: translateX(100%);
        transition: transform 0.3s ease;

        &.is-open {
          transform: translateX(0);
        }
      }

      &-link {
        color: #fff;
        font-weight: 500;
        font-size: 0.875rem;
        text-decoration: none;
        transition: color 0.2s;

        &--active,
        &:hover {
          color: $primary-color;
        }

        @include responsive(mobile) {
          font-size: 1rem;
          &--active,
          &:hover {
            color: $text-color;
          }
        }
      }
    }

    &__auth {
      display: flex;
      gap: 1.5rem;

      @include responsive(mobile) {
        position: fixed;
        bottom: 15%;
        left: 0;
        right: 0;
        justify-content: center;
        transform: translateX(100%);
        transition: transform 0.3s ease;

        &.is-open {
          transform: translateX(0);
        }
      }

      &-login {
        background: none;
        border: none;
        color: #fff;
        cursor: pointer;
        border-radius: 20px;
        transition: color 0.2s;
        font-size: 0.875rem;
        font-weight: 500;
        &:hover {
          color: $primary-color;
        }
        @include responsive(mobile) {
          font-size: 1rem;
        }
      }

      &-register {
        background: $primary-color;
        color: #fff;
        border: none;
        border-radius: 20px;
        padding: 0.5rem 1.5rem;
        cursor: pointer;
        transition: background 0.2s;
        font-size: 0.875rem;
        font-weight: 500;
        &:hover {
          background: $dark-orange;
        }

        @include responsive(mobile) {
          font-size: 1rem;
          background-color: $text-color;
          &:hover {
            background-color: $text-color;
          }
        }
      }
    }
  }
}
</style>
