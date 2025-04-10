<template>
    <nav class="navbar">
      <!-- Logo -->
      <div class="logo">
        <img src="@/assets/logo.png" alt="Orchestra Logo">
      </div>
      <ul class = "nav-links">
        <li @click="scrollTo('events-section')">{{ $t('event') }}</li>
        <li @click="scrollTo('about-section')">{{ $t('about') }}</li>
       <!---- <li>{{ $t('community') }}</li> -->
        <li @click="scrollTo('footer-section')">{{ $t('support') }}</li>
      </ul>

      

      <!-- Language Selection -->
      <div class="language-selector">
        <span
          v-for="lang in ['ru', 'kz', 'en']"
          :key="lang"
          :class="{ active: $i18n.locale === lang }"
          @click="$i18n.locale = lang"
        >
          {{ lang.toUpperCase() }}
        </span>
      </div>
    </nav>
  </template>
  
  <script>
  export default {
    name: "AppNavbar",
    data(){
      return {
        isBlackNavbar: false,
      };
    },
    methods: {
      scrollTo(sectionId) {
        const section = document.getElementById(sectionId);
        if (section) {
          section.scrollIntoView({ behavior: "smooth" });
        }
      },
      handleScroll() {
        this.isBlackNavbar = window.scrollY > window.innerHeight - 100;
      }
    },
    mounted(){
      window.addEventListener("scroll", this.handleScroll);
    },
    beforeUnmount() {
      window.removeEventListener("scroll", this.handleScroll);
    },
  };
  </script>
  