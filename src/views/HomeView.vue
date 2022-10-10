<template>
  <div class="home">
    <HeaderStore/>
    <HeroStore/>
    <BannerStore/>
    <InstaStore/>
    <LogoStore/>
    <FooterStore/>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderStore from "@/components/HeaderStore.vue";
import HeroStore from "@/components/HeroStore.vue";
import BannerStore from "@/components/BannerStore.vue";
import InstaStore from "@/components/InstaStore.vue";
import LogoStore from "@/components/LogoStore.vue";
import FooterStore from "@/components/FooterStore.vue";

export default {
  name: 'HomeView',
  components: {
    HeaderStore,
    HeroStore,
    BannerStore,
    InstaStore,
    LogoStore,
    FooterStore
  }
}
</script>
