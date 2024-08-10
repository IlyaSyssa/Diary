<template>
    <ion-fab vertical="bottom" horizontal="center" slot="fixed">
      <ion-fab-button>
        <ion-icon :icon="add"></ion-icon>
      </ion-fab-button>
    </ion-fab>
  </template>
  
  <script lang="ts">
    import { IonFab, IonFabButton, IonIcon } from '@ionic/vue';
    import { add } from 'ionicons/icons';
    import { defineComponent } from 'vue';
  
    export default defineComponent({
      components: { IonFab, IonFabButton, IonIcon },
      setup() {
        return { add };
      },
    });
  </script>
  
  <style>
    /* Дополнительные стили могут не понадобиться, если вы используете встроенные свойства Ionic */
  </style>
  