<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>
    <ion-refresher slot="fixed" @ionRefresh="handleRefresh($event)">
      <ion-refresher-content></ion-refresher-content>
    </ion-refresher>
    <Carousel paginationPosition="bottom-overlay" :paginationEnabled="true" :navigationEnabled="true"
            paginationActiveColor="var(--color-primary)" paginationColor="var(--tw-prose-body)" class="h-full w-full"
            :perPage="1" :loop="true">
            <slide v-for="image of carouselImages" :key="image" class="h-full">
              <img :src="image" class="mt-0 mb-0 h-full w-full object-cover" />
            </slide>
          </Carousel>
      <div id="container">
        <strong>Ready to create an app?</strong>
        <p>Start with Ionic <a target="_blank" rel="noopener noreferrer" href="https://ionicframework.com/docs/components">UI Components</a></p>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonRefresher, IonRefresherContent, onIonViewDidEnter } from '@ionic/vue';
import { ref } from 'vue';
import { Carousel, Slide } from '@jambonn/vue-concise-carousel';
import '@jambonn/vue-concise-carousel/lib/vue-concise-carousel.css';

const carouselImages = ref<string[] | null>(null)

const carouselBaseData = [
  "https://pngimg.com/uploads/pokemon/pokemon_PNG129.png",
  "https://pngimg.com/uploads/pokemon/pokemon_PNG123.png"
  ]

  onIonViewDidEnter(() => {
    carouselImages.value = carouselBaseData.map((image) => {
      return image
    })
  })

  const handleRefresh = (event: CustomEvent) => {
    carouselImages.value = null;
    setTimeout(() => {
    carouselImages.value = [...carouselBaseData].sort(() => Math.random() - 0.5);
    (event.target as any).complete();
    }, 500);
  }
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
