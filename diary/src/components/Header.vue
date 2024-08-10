<template>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Дневник</ion-title>
        <img class="diaryImg" src="./images/Apple_Journal_-_App_Icon_-_iOS17.png"
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Дневник</ion-title>
        </ion-toolbar>
      </ion-header>
  
      <div class="ion-padding">
        <ion-card>
      <ion-card-header>
        <ion-card-title>Название</ion-card-title>
        <ion-card-subtitle>Ваша запись</ion-card-subtitle>
      </ion-card-header>
  
      <ion-card-content>
        Введите текст
      </ion-card-content>
    </ion-card>
      </div>
    </ion-content>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  import { IonContent, IonHeader, IonTitle, IonToolbar, IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle } from '@ionic/vue';

  export default defineComponent({
    components: {
      IonContent,
      IonHeader,
      IonTitle,
      IonToolbar,
      IonCard,
      IonCardContent,
      IonCardHeader,
      IonCardSubtitle,
      IonCardTitle
    },
  });
</script>

<style>
  .diaryImg {
    width: 70px;
  }
</style>