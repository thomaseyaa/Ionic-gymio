<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="danger">
        <ion-title>Gymio</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-padding-top">
      <div>
        <form method="POST" @submit.prevent="toReserve">
          <ion-text>
           <h1 class="ion-text-center"><strong>Réservation</strong></h1>
          </ion-text>

          <ion-item>
            <ion-label>Email:</ion-label>
            <ion-input name="email" type="email" v-model="form.email"></ion-input>
          </ion-item>
          <ion-item>
            <ion-label>Date:</ion-label>
            <ion-input name="date" type="date" v-model="form.date"></ion-input>
          </ion-item>
          <ion-item>
            <ion-label>Heure:</ion-label>
            <ion-input name="time" type="time" v-model="form.time"></ion-input>
          </ion-item>
          <ion-item>
            <ion-label>CGU</ion-label>
            <ion-checkbox name="cgu" color="danger">Accepter les conditions d'utilisation</ion-checkbox>
          </ion-item>
          <br>

          <ion-button type="submit" color="danger" class="ion-padding-horizontal">Réserver</ion-button>
        </form>

        <ion-text class="ion-text-center" color="success" v-if="msg.success">
          <p>{{ msg.success }}</p>
        </ion-text>

        <ion-text class="ion-text-center" color="danger" v-if="msg.error">
          <p>{{ msg.error }}</p>
        </ion-text>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonLabel, IonInput, IonCheckbox, IonButton } from '@ionic/vue';

export default  {
  components: { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonLabel, IonInput, IonCheckbox, IonButton },

  name: 'Reservation',
  data(){
    return{
      form: {
        email: "",
        date: "",
        time: "",
      },
      msg: "",
    }
  },
  methods: {
    toReserve(){
      fetch(`https://gym-affluences.herokuapp.com/api/reservation`,{
        method: 'POST',
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.form)
      })
          .then(response => response.json())
          .then(data => {
            console.log(data);
            this.msg = data
            if(this.msg.success){
              this.form.email = "";
              this.form.date = "";
              this.form.time = "";
            }
          })
          .catch(function (error){
            console.log(error);
          });
    },
  },
}
</script>