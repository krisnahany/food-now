<template>
  <!-- Footer -->
  <footer class="footer">
    <div class="footer-content">
      <div class="footer-section">
        <div class="footer-brand">
          <div class="footer-brand__title">
            <img :src="logo" alt="logo" width="215" height="38" />
          </div>
          <div>
            <p class="footer-brand__subtitle">Find Us :</p>
            <div class="footer-brand__social">
              <a href="#" class="footer-brand__social-link">
                <img :src="facebook" alt="facebook" width="24" height="24" />
              </a>
              <a href="#" class="footer-brand__social-link">
                <img :src="instagram" alt="instagram" width="24" height="24" />
              </a>
              <a href="#" class="footer-brand__social-link">
                <img :src="youtube" alt="youtube" width="24" height="24" />
              </a>
            </div>
          </div>
        </div>
      </div>

      <div class="footer-section">
        <h4 class="footer-section__title">Navigation</h4>
        <ul class="footer-section__list">
          <li><a href="#" class="footer-section__link">Home</a></li>
          <li><a href="#" class="footer-section__link">Order</a></li>
          <li><a href="#" class="footer-section__link">About</a></li>
          <li><a href="#" class="footer-section__link">Blog</a></li>
          <li><a href="#" class="footer-section__link">Contact</a></li>
          <li><a href="#" class="footer-section__link">Login</a></li>
          <li><a href="#" class="footer-section__link">Register</a></li>
        </ul>
      </div>

      <div class="footer-section">
        <h4 class="footer-section__title">Contact</h4>
        <ul class="footer-contact">
          <li class="footer-contact__item">
            <a href="mailto:Food.now@mail.com" class="footer-contact__link">
              <img :src="mail" alt="mail" width="24" height="24" />
              Food.now@mail.com
            </a>
          </li>
          <li class="footer-contact__item">
            <a href="tel:+62848477102943" class="footer-contact__link">
              <img :src="phone" alt="phone" width="24" height="24" />
              +62848477102943
            </a>
          </li>
          <li class="footer-contact__item">
            <a href="tel:+62818493849494" class="footer-contact__link">
              <img :src="whatsapp" alt="whatsapp" width="24" height="24" />
              +62818493849494
            </a>
          </li>
        </ul>
      </div>

      <div class="footer-section">
        <h4 class="footer-section__title">Location</h4>
        <div class="footer-location">
          <div class="footer-location__icon">
            <img :src="location" alt="location" width="24" height="24" />
          </div>
          <div>
            <p class="footer-location__name">Kerobokan</p>
            <p class="footer-location__address">
              Jl. Raya Kerobokan Br Taman, Kuta No.98, Kerobokan Kelod, Kec. Kuta Utara, Kabupaten
              Badung, Bali 80361
            </p>
          </div>
        </div>
      </div>
    </div>

    <div class="copyright">
      <p class="copyright__text">
        Copyright © 2022 Foodnow. All Rights Reserved. Powered by PT. Timedoor Indonesia. |
        <a href="#" class="copyright__link">Privacy Policy</a>
      </p>
      <p class="copyright__text">
        This site is protected by reCAPTCHA and the Google Privacy Policy and Terms of Service
        apply.
      </p>
    </div>
  </footer>
</template>

<script setup>
import logo from "/assets/img/logo-alt.svg";
import facebook from "/assets/img/icons/facebook.svg";
import instagram from "/assets/img/icons/instagram.svg";
import youtube from "/assets/img/icons/youtube.svg";
import mail from "/assets/img/icons/mail.svg";
import phone from "/assets/img/icons/phone.svg";
import whatsapp from "/assets/img/icons/whatsapp.svg";
import location from "/assets/img/icons/location.svg";
</script>

<style lang="scss" scoped>
@use "@/assets/scss/variables.scss" as *;
@use "@/assets/scss/mixins.scss" as *;

.footer {
  color: $text-color;
  @include container;

  &-content {
    border-top: 1px solid $border-color;
    border-bottom: 1px solid $border-color;
    padding: 40px 0 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);

    @include responsive(tablet) {
      grid-template-columns: repeat(2, 1fr);
      gap: 30px;
    }

    @include responsive(mobile) {
      grid-template-columns: 1fr;
      gap: 20px;
    }
  }

  &-section {
    &:first-child {
      display: flex;
      align-items: center;
    }
    &__title {
      color: $primary-color;
      font-size: 1.125rem;
      font-weight: 600;
      margin-bottom: 15px;
    }

    &__list {
      list-style: none;
      display: grid;
      grid-auto-flow: column;
      grid-template-rows: repeat(4, 1fr);
      font-size: 0.875rem;
      row-gap: 5px;
      grid-template-columns: 100px;
    }

    &__link {
      color: $text-color;
      text-decoration: none;
      @include transition;

      &:hover {
        color: $primary-color;
      }
    }

    @include responsive(mobile) {
      &__list {
        grid-template-columns: auto;
        grid-template-rows: repeat(2, 1fr);
      }
    }
  }

  &-brand {
    display: flex;
    flex-direction: column;
    gap: 30px;
    width: 100%;

    &__title {
      & > img {
        height: 2rem;
        width: auto;
        max-width: 100%;
      }
    }

    &__subtitle {
      margin-bottom: 10px;
      font-size: 1rem;
      font-weight: 700;
      color: $primary-color;
    }

    &__social {
      display: flex;
      gap: 10px;
    }

    &__social-link {
      width: 2.25rem;
      height: 2.25rem;
      border: 1px solid $primary-color;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      text-decoration: none;
      @include transition;
      background: transparent;

      & > img {
        width: 1.2rem;
        height: 1.2rem;
        vertical-align: middle;
      }

      &:hover {
        background: $secondary-color;
        border-color: $primary-color;
      }
    }

    @include responsive(mobile) {
      &__title {
        text-align: center;
        & > img {
          height: 2rem;
        }
      }

      &__subtitle {
        font-size: 1.125rem;
        font-weight: 600;
      }
    }
  }

  &-contact {
    list-style: none;
    &__item {
      margin-bottom: 5px;
      color: $text-color;
      font-size: 0.875rem;
    }

    &__link {
      display: flex;
      align-items: center;
      gap: 5px;
      line-height: 1.5;
      color: $text-color;
      text-decoration: none;
      @include transition;

      img {
        height: 1.2em;
        width: auto;
      }

      &:hover {
        color: $primary-color;
      }
    }
  }

  &-location {
    display: flex;
    gap: 4px;

    &__icon {
      & > img {
        height: 1.2em;
        width: auto;
      }
    }

    &__name {
      font-weight: 600;
      font-size: 0.875rem;
      line-height: 1.3;
      margin-bottom: 2px;
    }

    &__address {
      color: $text-color;
      font-size: 0.875rem;
      line-height: 1.5;
    }
  }
}

.copyright {
  padding: 20px 0;
  text-align: center;

  &__text {
    color: $text-color;
    font-size: 0.875rem;

    &:last-child {
      font-size: 0.75rem;
      margin-top: 5px;
    }
  }

  &__link {
    color: $text-color;
    text-decoration: none;
    @include transition;

    &:hover {
      color: $primary-color;
    }
  }

  @include responsive(mobile) {
    &__text {
      font-size: 0.625rem;
      &:last-child {
        font-size: 0.563rem;
      }
    }
  }
}
</style>
