<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
 
        <!-- botão voltar -->
        <ion-buttons slot="start">
          <ion-back-button default-href="/"></ion-back-button>
        </ion-buttons>
 
        <ion-title>Tarefas</ion-title>
 
      </ion-toolbar>
    </ion-header>
 
    <ion-content class="ion-padding">
 
      <!-- Card adicionar -->
      <ion-card>
        <ion-card-header>
          <ion-card-title>Nova tarefa</ion-card-title>
        </ion-card-header>
 
        <ion-card-content>
 
          <ion-item>
            <ion-input
              v-model="novaTarefa"
              placeholder="Digite sua tarefa..."
              clear-input
            ></ion-input>
 
            <ion-button slot="end" @click="adicionarTarefa">
              Adicionar
            </ion-button>
          </ion-item>
 
          <ion-text color="danger" v-if="erro">
            <p class="erro">Digite uma tarefa válida.</p>
          </ion-text>
 
        </ion-card-content>
      </ion-card>
 
      <!-- Lista -->
      <ion-card v-if="tarefas.length > 0">
        <ion-card-header>
          <ion-card-title>Minhas tarefas</ion-card-title>
        </ion-card-header>
 
        <ion-list>
 
          <ion-item
            v-for="(tarefa, index) in tarefas"
            :key="index"
            class="tarefa-item"
          >
            <ion-label>
              {{ tarefa }}
            </ion-label>
 
            <ion-button
              fill="clear"
              color="danger"
              slot="end"
              @click="removerTarefa(index)"
            >
              Remover
            </ion-button>
 
          </ion-item>
 
        </ion-list>
      </ion-card>
 
      <div v-if="tarefas.length === 0" class="empty">
        <ion-text color="medium">
          <p>Nenhuma tarefa adicionada ainda.</p>
        </ion-text>
      </div>
 
    </ion-content>
  </ion-page>
</template>
 
<script setup lang="ts">
import { ref } from 'vue'
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonItem,
  IonInput,
  IonButton,
  IonList,
  IonLabel,
  IonText,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonButtons,
  IonBackButton
} from '@ionic/vue'
 
const novaTarefa = ref('')
const tarefas = ref<string[]>([])
const erro = ref(false)
 
const adicionarTarefa = () => {
  if (novaTarefa.value.trim() === '') {
    erro.value = true
    return
  }
 
  tarefas.value.push(novaTarefa.value)
  novaTarefa.value = ''
  erro.value = false
}
 
const removerTarefa = (index: number) => {
  tarefas.value.splice(index, 1)
}
</script>
 
<style scoped>
 
ion-card{
  margin-bottom: 20px;
}
 
.tarefa-item{
  --padding-start: 10px;
  --inner-padding-end: 10px;
}
 
.erro{
  margin-top: 8px;
  font-size: 14px;
}
 
.empty{
  text-align: center;
  margin-top: 40px;
  opacity: 0.7;
}
 
</style>