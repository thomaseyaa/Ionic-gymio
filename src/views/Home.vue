<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="danger">
        <ion-title>Gymio</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <div v-for="item in items" :key="item.src">
        <ion-img :src="item.src"></ion-img>
      </div>

      <div class="ion-padding-horizontal">
        <ion-text>
          <h1><strong>Bienvenu sur Gymio</strong></h1>
        </ion-text>

        <ion-text>
          <h5>Ouvert du lundi au vendredi de {{ openingHour }}h à {{ closingHour }}h.</h5>
        </ion-text>

        <ion-text color="medium">
          <h5>Suite à l'épidemie de la Covid-19 nous restreignons l'accès à notre salle de sport. Réservez un crénaux pour pourvoir vous entrainer (vous ne pouvez reserver que {{ reservationLimit }} crénaux par semaine).</h5>
        </ion-text>

        <ion-text>
          <ion-router-link color="danger" href="/tabs/tab2">Resérver</ion-router-link>
        </ion-text>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonImg } from '@ionic/vue';

export default  {
  components: { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonImg },

  setup() {
    const items = [{
      'text': 'Item 1',
      'src': '/assets/img/hero1.png'
    }];
    return { items }
  },

  name: 'Home',
  data(){
    return{
      openingHour: "",
      closingHour: "",
      reservationLimit: "",
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
            this.reservationLimit = data.reservationLimit;
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