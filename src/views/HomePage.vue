```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title>📸 Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="gallery-content">
      <div class="welcome-section">
        <h1>My Photo Gallery</h1>
        <p>Capture and keep your favorite memories.</p>
      </div>

      <div class="gallery-grid">
        <div
          v-for="photo in photos"
          :key="photo.id"
          class="photo-card"
        >
          <img :src="photo.url" :alt="photo.title" />

          <div class="photo-info">
            <strong>{{ photo.title }}</strong>
            <span>{{ photo.date }}</span>
          </div>
        </div>
      </div>

      <div v-if="photos.length === 0" class="empty-gallery">
        <div class="empty-icon">📷</div>
        <h2>No Photos Yet</h2>
        <p>Your photos will appear here.</p>
      </div>
    </ion-content>

    <ion-fab vertical="bottom" horizontal="end" slot="fixed">
      <ion-fab-button color="primary" @click="addPhoto">
        <ion-icon :icon="add"></ion-icon>
      </ion-fab-button>
    </ion-fab>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonFab,
  IonFabButton,
  IonIcon
} from '@ionic/vue';

import { add } from 'ionicons/icons';
import { ref } from 'vue';

const photos = ref([
  {
    id: 1,
    title: 'Nature',
    date: 'September 15, 2026',
    url: 'https://images.unsplash.com/photo-1500534623283-312aade485b7?auto=format&fit=crop&w=800&q=80'
  },
  {
    id: 2,
    title: 'Mountain',
    date: 'September 15, 2026',
    url: 'https://images.unsplash.com/photo-1464822759023-fed622ff2c3b?auto=format&fit=crop&w=800&q=80'
  },
  {
    id: 3,
    title: 'Beach',
    date: 'September 15, 2026',
    url: 'https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=800&q=80'
  },
  {
    id: 4,
    title: 'Sunset',
    date: 'September 15, 2026',
    url: 'https://images.unsplash.com/photo-1470252649378-9c29740c9fa8?auto=format&fit=crop&w=800&q=80'
  }
]);

const addPhoto = () => {
  alert('Photo Gallery is ready! The Add Photo feature can be connected to the device camera next.');
};
</script>

<style scoped>
.gallery-content {
  --background: #f4f6f8;
}

.welcome-section {
  text-align: center;
  padding: 28px 20px 18px;
}

.welcome-section h1 {
  margin: 0 0 8px;
  font-size: 28px;
  font-weight: 700;
}

.welcome-section p {
  margin: 0;
  color: #666;
  font-size: 15px;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 14px;
  padding: 10px 16px 90px;
}

.photo-card {
  background: white;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.12);
}

.photo-card img {
  display: block;
  width: 100%;
  height: 180px;
  object-fit: cover;
}

.photo-info {
  display: flex;
  flex-direction: column;
  gap: 4px;
  padding: 12px;
}

.photo-info strong {
  font-size: 16px;
  color: #222;
}

.photo-info span {
  font-size: 12px;
  color: #777;
}

.empty-gallery {
  text-align: center;
  padding: 80px 20px;
  color: #777;
}

.empty-icon {
  font-size: 60px;
  margin-bottom: 15px;
}

.empty-gallery h2 {
  color: #333;
  margin-bottom: 8px;
}

.empty-gallery p {
  margin: 0;
}
</style>
```
