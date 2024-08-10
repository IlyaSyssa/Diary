<template>
  <ion-header :translucent="true">
    <ion-toolbar>
      <ion-title>Дневник</ion-title>
      <img class="diaryImg" src="./images/Apple_Journal_-_App_Icon_-_iOS17.png">
    </ion-toolbar>
  </ion-header>
  
  <ion-content :fullscreen="true">
    <ion-header collapse="condense">
      <ion-toolbar>
        <ion-title size="large">Дневник</ion-title>
      </ion-toolbar>
    </ion-header>
  
    <div class="ion-padding" v-for="(card, index) in cards" :key="index">
      <ion-card>
        <ion-card-header>
          <ion-card-title>{{ card.title }}</ion-card-title>
          <ion-card-subtitle>{{ card.subtitle }}</ion-card-subtitle>
        </ion-card-header>
        <ion-card-content>
          {{ card.content }}
        </ion-card-content>
      </ion-card>
    </div>
  </ion-content>
  
  <ion-fab vertical="bottom" horizontal="center" slot="fixed">
    <ion-fab-button @click="addCard">
      <ion-icon :icon="add"></ion-icon>
    </ion-fab-button>
  </ion-fab>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { add } from 'ionicons/icons';
import { IonContent, IonHeader, IonTitle, IonToolbar, IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle, IonFab, IonFabButton, IonIcon } from '@ionic/vue';

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
    IonCardTitle,
    IonFab,
    IonFabButton,
    IonIcon
  },
  setup() {
    const cards = ref([
      {
        title: "Название ",
        subtitle: "Ваша запись 1",
        content: "Введите текст ",
      }
    ]);

    const addCard = () => {
      const newCard = {
        title: `Название`,
        subtitle: `Ваша запись ${cards.value.length + 1}`,
        content: `Введите текст`,
      };
      cards.value.push(newCard);
    };

    return { add, cards, addCard };
  },
});
</script>

<style>
  .diaryImg {
    width: 70px;
  }
</style>
