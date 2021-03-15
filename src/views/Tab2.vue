<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Réservation</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header>
        <ion-card color="success">
          <p v-if="msg.success">{{ msg.success }}</p>
        </ion-card>
        <ion-card color="danger">
          <p v-if="msg.error">{{ msg.error }}</p>
        </ion-card>
        <form method="POST" @submit.prevent="toReserve">
          <div>
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
              <ion-checkbox name="cgu">Accepter les conditions d'utilisation</ion-checkbox>
            </ion-item>
            <ion-button type="submit">Réserver</ion-button>
          </div>
        </form>
      </ion-header>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCard, IonItem, IonLabel, IonInput, IonCheckbox, IonButton } from '@ionic/vue';

export default  {
  components: { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCard, IonItem, IonLabel, IonInput, IonCheckbox, IonButton },

  name: 'Tab2',
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
      fetch(`http://gym-affluences.herokuapp.com/api/reservation`,{
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