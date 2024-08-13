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
      <ion-toggle @click="toggleDarkTheme">Default Toggle</ion-toggle>
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
      
      <!-- Передаём индекс карточки в метод удаления -->
      <ion-button fill="outline" @click="deleteCard(index)">Удалить запись</ion-button>
    </div>
  </ion-content>
  
  <ion-fab vertical="bottom" horizontal="center" slot="fixed">
    <ion-fab-button @click="addCard">
      <ion-icon :icon="add"></ion-icon>
    </ion-fab-button>
  </ion-fab>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, watch } from 'vue';
import { add } from 'ionicons/icons';
import { IonContent, IonHeader, IonTitle, IonToolbar, IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle, IonFab, IonFabButton, IonIcon, IonButton, IonToggle } from '@ionic/vue';

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
    IonIcon,
    IonButton,
    IonToggle
  },
  setup() {
    const cards = ref([]);

    const toggleDarkTheme = (e) => {
      console.log(e)
      document.body.classList.toggle('dark');
      document
                .querySelector('meta[name="theme-color"]')
                ?.setAttribute("content", e.detail.checked ? "#000" : "#f7f7f7");
    };

    // Загрузка данных из LocalStorage при загрузке приложения
    onMounted(() => {
      const savedCards = localStorage.getItem('cards');
      if (savedCards) {
        cards.value = JSON.parse(savedCards);
      }
    });

    // Сохранение данных в LocalStorage при изменении карточек
    watch(cards, (newCards) => {
      localStorage.setItem('cards', JSON.stringify(newCards));
    }, { deep: true });

    const addCard = () => {
      cards.value.push({
        title: "Название",
        subtitle: "Ваша запись",
        content: "Введите текст",
        isEditing: false,
      });
    };

    const deleteCard = (index: number) => {
      cards.value.splice(index, 1);
    };

    const editCard = (index: number) => {
      cards.value[index].isEditing = true;
    };

    const saveCard = (index: number) => {
      cards.value[index].isEditing = false;
    };

    return { add, cards, addCard, editCard, saveCard, deleteCard, toggleDarkTheme };
}
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
