<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="danger">
        <ion-title>Gymio</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-item v-for="item in items" :key="item.src">
        <ion-img :src="item.src" width="100"></ion-img>
      </ion-item>

      <div>
        <ion-card>
          <ion-card-header>
            <ion-card-title>Bienvenu sur Gymio </ion-card-title>
          </ion-card-header>
          <ion-card-header>
            <ion-card-subtitle>Ouvert du lundi au vendredi de {{ openingHour }}h à {{ closingHour }}h</ion-card-subtitle>
            <br>
            <ion-card-subtitle>Suite à l'épidemie de la Covid-19 nous restreignons l'accès à notre salle de sport. Réservez un crénaux pour pourvoir vous entrainer.</ion-card-subtitle>
          </ion-card-header>
        </ion-card>
      </div>

    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonImg, IonCard, IonCardHeader, IonCardTitle, IonCardSubtitle } from '@ionic/vue';

export default  {
  components: { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonImg, IonCard, IonCardHeader, IonCardTitle, IonCardSubtitle },

  setup() {
    const items = [{
      'text': 'Item 1',
      'src': '/assets/img/hero1.png'
    }];
    return { items }
  },

  name: 'Tab1',
  data(){
    return{
      openingHour: "",
      closingHour: "",
    }
  },
  methods: {
    showInfo(){
      fetch(`http://gym-affluences.herokuapp.com/api/infos`)
          .then(response => response.json())
          .then(data => {
            console.log(data);
            this.openingHour = data.openingHour;
            this.closingHour = data.closingHour;
          })
          .catch(function (error){
            console.log(error);
          });
    },
  },
  mounted(){
    this.showInfo();
  },
}
</script>