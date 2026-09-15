<template>
  <ion-page>
    <!-- HEADER -->
    <ion-header>
      <ion-toolbar class="pink-toolbar">
        <ion-title>My Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="page-content">

      <!-- CAMERA SECTION -->
      <div class="camera-section">
        <h2>Camera</h2>

        <ion-button
          expand="block"
          class="take-picture-button"
          @click="takePicture"
        >
          <ion-icon
            slot="start"
            :icon="cameraIcon"
          ></ion-icon>

          TAKE PICTURE
        </ion-button>

        <!-- Error message -->
        <p v-if="errorMessage" class="error-message">
          {{ errorMessage }}
        </p>
      </div>


      <!-- PHOTO GALLERY -->
      <div class="gallery-section">

        <div class="gallery-title">
          Photo Gallery
        </div>

        <!-- EMPTY GALLERY -->
        <div
          v-if="photos.length === 0"
          class="empty-gallery"
        >
          <div class="camera-symbol">
            📷
          </div>

          <p>No photos yet.</p>

          <span>
            Take a picture using the camera.
          </span>
        </div>


        <!-- PHOTOS -->
        <div
          v-else
          class="photo-grid"
        >
          <div
            v-for="(photo, index) in photos"
            :key="index"
            class="photo-card"
          >
            <img
              :src="photo"
              alt="Captured photo"
            />

            <p>Photo {{ index + 1 }}</p>
          </div>
        </div>

      </div>

    </ion-content>
  </ion-page>
</template>


<script setup lang="ts">

import { ref } from 'vue';

import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButton,
  IonIcon
} from '@ionic/vue';

import { camera as cameraIcon } from 'ionicons/icons';

import {
  Camera,
  CameraResultType,
  CameraSource
} from '@capacitor/camera';


// Store captured photos
const photos = ref<string[]>([]);


// Error message
const errorMessage = ref('');


// TAKE PICTURE
const takePicture = async () => {

  try {

    // Clear previous error
    errorMessage.value = '';

    // Open the PHONE CAMERA
    const image = await Camera.getPhoto({

      quality: 90,

      allowEditing: false,

      resultType: CameraResultType.DataUrl,

      source: CameraSource.Camera

    });


    // Add captured photo to gallery
    if (image.dataUrl) {

      photos.value.push(image.dataUrl);

    }

  } catch (error: any) {

    console.log('Camera error:', error);

    // Don't show an error if user simply cancelled the camera
    if (
      error?.message &&
      !error.message.toLowerCase().includes('cancel')
    ) {

      errorMessage.value =
        'Unable to open the camera. Please check the camera permission.';

    }

  }

};

</script>


<style scoped>

/* ============================= */
/* MAIN PAGE */
/* ============================= */

.page-content {
  --background: #fff5fa;
}


/* ============================= */
/* HEADER */
/* ============================= */

.pink-toolbar {
  --background: #ff69b4;
  --color: white;
}

ion-title {
  font-size: 20px;
  font-weight: 700;
}


/* ============================= */
/* CAMERA SECTION */
/* ============================= */

.camera-section {
  padding: 24px 20px 15px;
}

.camera-section h2 {
  margin: 0 0 12px;

  font-size: 18px;

  font-weight: 700;

  color: #d63384;
}


/* ============================= */
/* TAKE PICTURE BUTTON */
/* ============================= */

.take-picture-button {

  --background: #ff69b4;

  --background-hover: #ff4fa3;

  --background-activated: #e7549f;

  --color: white;

  --border-radius: 8px;

  height: 46px;

  margin: 0;

  font-weight: 700;

  letter-spacing: 0.5px;

}


/* ============================= */
/* ERROR MESSAGE */
/* ============================= */

.error-message {

  margin-top: 10px;

  text-align: center;

  color: #d63384;

  font-size: 13px;

}


/* ============================= */
/* GALLERY CONTAINER */
/* ============================= */

.gallery-section {

  margin: 12px 20px;

  background: white;

  border: 2px solid #ffb6d9;

  border-radius: 10px;

  min-height: 320px;

  overflow: hidden;

  box-shadow:
    0 3px 10px
    rgba(255, 105, 180, 0.12);

}


/* ============================= */
/* GALLERY TITLE */
/* ============================= */

.gallery-title {

  padding: 15px;

  font-size: 18px;

  font-weight: 700;

  color: #d63384;

  background: #ffe1ef;

  border-bottom: 2px solid #ffb6d9;

}


/* ============================= */
/* EMPTY GALLERY */
/* ============================= */

.empty-gallery {

  text-align: center;

  padding: 70px 20px;

}


/* Camera icon */

.camera-symbol {

  font-size: 45px;

  margin-bottom: 12px;

}


/* No photos text */

.empty-gallery p {

  margin: 0 0 8px;

  font-size: 17px;

  font-weight: 600;

  color: #d63384;

}


/* Instruction */

.empty-gallery span {

  font-size: 14px;

  color: #999;

}


/* ============================= */
/* PHOTO GRID */
/* ============================= */

.photo-grid {

  display: grid;

  grid-template-columns:
    repeat(2, 1fr);

  gap: 12px;

  padding: 12px;

}


/* ============================= */
/* PHOTO CARD */
/* ============================= */

.photo-card {

  background: #fff5fa;

  border: 2px solid #ffb6d9;

  border-radius: 8px;

  overflow: hidden;

}


/* Captured image */

.photo-card img {

  display: block;

  width: 100%;

  height: 180px;

  object-fit: cover;

}


/* Photo number */

.photo-card p {

  margin: 0;

  padding: 8px;

  text-align: center;

  font-size: 13px;

  font-weight: 600;

  color: #d63384;

}

</style>