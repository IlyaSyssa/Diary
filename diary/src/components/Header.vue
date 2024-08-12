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
      <ion-card @click="editCard(index)">
        <ion-card-header>
          <ion-card-title v-if="!card.isEditing">{{ card.title }}</ion-card-title>
          <input v-else v-model="card.title" @blur="saveCard(index)" />
          
          <ion-card-subtitle v-if="!card.isEditing">{{ card.subtitle }}</ion-card-subtitle>
          <textarea v-else v-model="card.subtitle" @blur="saveCard(index)" />
        </ion-card-header>
        
        <ion-card-content v-if="!card.isEditing">
          {{ card.content }}
        </ion-card-content>
        <textarea v-else v-model="card.content" @blur="saveCard(index)" />
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
        title: "Название 1",
        subtitle: "Ваша запись 1",
        content: "Введите текст 1",
        isEditing: false,
      }
    ]);

    const addCard = () => {
      cards.value.push({
        title: "Название",
        subtitle: "Ваша запись",
        content: "Введите текст",
        isEditing: false,
      });
    };

    const editCard = (index: number) => {
      cards.value[index].isEditing = true;
    };

    const saveCard = (index: number) => {
      cards.value[index].isEditing = false;
    };

    return { add, cards, addCard, editCard, saveCard };
  },
});
</script>

<style>
  .diaryImg {
    width: 70px;
  }
  input, textarea {
    width: 100%;
  }
</style>
