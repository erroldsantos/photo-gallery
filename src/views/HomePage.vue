<template>
  <ion-page class="gallery-page">
    <ion-header class="ion-no-border">
      <!-- Applying #6D639C for header accent and #1E1A33 for depth -->
      <ion-toolbar class="toolbar-accent">
        <ion-title>My Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <!-- Applying the darkest color #141633 as the full background -->
    <ion-content class="ion-padding gallery-content">
      <div class="main-layout">
        <section class="camera-section">
          <CameraComponent @photo-captured="addPhoto" />
        </section>

        <section class="gallery-section">
          <PhotoGalleryComponent :photos="photos" />
        </section>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";
import { ref } from "vue";
import CameraComponent from "@/components/CameraComponent.vue";
import PhotoGalleryComponent from "@/components/PhotoGalleryComponent.vue";

const photos = ref<string[]>([]);
const addPhoto = (photo: string) => {
  photos.value.unshift(photo);
};
</script>

<style scoped>
/* Define the palette for component usage */
:root {
  --color-lavender: #9D7498;    /* Left mauve */
  --color-dusty-mauve: #74546D; /* 2nd mauve */
  --color-deep-navy: #1E1A33;  /* 3rd (darker) navy */
  --color-highlight: #6D639C;  /* 4th (lighter) purple-navy */
  --color-midnight: #141633;   /* Right (darkest) navy */
}

/* Page content background using darkest midnight blue */
.gallery-content {
  --background: #141633;
  --color: #ffffff;
}

/* Toolbar using lighter purple-navy highlight with gradient */
.toolbar-accent {
  --background: linear-gradient(135deg, #6D639C 0%, #1E1A33 100%);
  --color: #ffffff;
}

/* Centered layout with limited width */
.main-layout {
  max-width: 720px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* Base style overrides for imported components (cards, etc.) */
:deep(ion-card) {
  --background: #1E1A33; /* Cards use deep navy */
  --color: #ffffff;
  border: 1px solid #74546D; /* Cards border matches dusty mauve */
}

:deep(ion-button) {
  --background: #6D639C; /* Buttons use the highlight purple */
  --color: #ffffff;
}
</style>