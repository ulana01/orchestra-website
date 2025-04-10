<template>
  <div>
    <AppNavbar />
    <HeroSection />
    <EventsSection />
    <TheShow />
    <AboutUs />
    <FooterSection />
  </div>
</template>

<script>
import AppNavbar from './components/AppNavbar.vue';
import HeroSection from './components/HeroSection.vue';
import EventsSection from './components/EventsSection.vue';
import TheShow from './components/TheShow.vue';
import AboutUs from './components/AboutUs.vue'; 
import FooterSection from './components/FooterSection.vue'

export default {
  components: {
    AppNavbar,
    HeroSection,
    EventsSection,
    TheShow,
    AboutUs,
    FooterSection, 
  }
};
</script>
