<template>
  <ion-page>
    <ion-tabs>
      <ion-tab-bar slot="bottom" color="danger">
        <ion-tab-button tab="home" href="/tabs/home">
          <ion-icon :icon="homeOutline" />
          <ion-label>Accueil</ion-label>
        </ion-tab-button>
          
        <ion-tab-button tab="reservation" href="/tabs/reservation">
          <ion-icon :icon="calendarOutline" />
          <ion-label>Réservation</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script>
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage } from '@ionic/vue';
import { homeOutline, calendarOutline } from 'ionicons/icons';

export default {
  name: 'Tabs',
  components: { IonLabel, IonTabs, IonTabBar, IonTabButton, IonIcon, IonPage },
  setup() {
    return {
      homeOutline,
      calendarOutline,
    }
  }
}
</script>