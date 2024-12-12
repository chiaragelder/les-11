<template>
  <div class="layout1">
    <ClientOnly>
      <!-- Drawer -->
      <div class="pr-5 z-100">
        <Drawer />
      </div>

      <!-- Main content -->
      <div> 
        <!-- Text content container -->
        <div class="text-container flex items-start">
          <!-- Titel aan de linkerkant -->
          <h1 class="text-3xl md:text-3xl lg:text-6xl lg:mb-10 font-bold mr-8 max-w-2xl">{{ data.title }}</h1>
          
          <!-- Rest van de tekst -->
          <div class="text-content">
            <p class="text-lg md:text-2xl lg:text-xl pb-10 font-bold">{{ data.description }}</p>
            <ContentRenderer :value="data" />
          </div>
        </div>
        
        <!-- Image gallery -->
        <div v-if="data.imagegallery && data.imagegallery.showgallery == true" class="pt-16 pb-24 gallery-container">
          <div class="image-gallery-padding">
            <ImageGallery />
          </div>
        </div>

        <!-- Metadata and tags -->
        <div class="text-xs leading-3 container">
          <hr />
          <p class="text-xs opacity-50 hover:opacity-100 pb-5">Last update: {{ formatDate(data.date) }}</p>
          <article v-if="data.tags" class="tags">
            <li v-for="(item, index) in data.tags" :key="index" class="pt-2 text-xs opacity-50 hover:opacity-100">
              <NuxtLink :to="`/tags/${item}`">{{ item }}</NuxtLink>
            </li>
          </article>
        </div>
      </div>

      <!-- Share Buttons -->
      <ShareButtons />
    
      <!-- SEO metadata -->
      <Title>{{ data.title }}</Title>
      <Meta name="description" :content="data.description" />
      <Meta name="tags" :content="data.tags" />
      <Meta name="keywords" :content="data.tags.join(', ')" />
      <Meta property="og:title" :content="data.title" />
      <Meta property="og:description" :content="data.description" />
      <Meta property="og:image" :content="data.thumbnail" />
      <Meta property="og:url" :content="data.url" />
      <Meta property="og:type" content="article" />
    </ClientOnly>
  </div>
</template>

<style>
/* Styling for the text container */
.text-container {
  max-width: 1200px; /* Verhoog de maximale breedte van de tekst */
  margin: 0 auto; /* Centreer de container */
  padding: 16px; /* Voeg padding toe rond de tekst */
  margin-left: 100px; /* Dit voegt extra ruimte aan de linkerzijde toe */
  display: flex; /* Gebruik flexbox om de titel en tekst naast elkaar te plaatsen */
  align-items: flex-start; /* Zorg ervoor dat de titel en tekst aan de bovenkant worden uitgelijnd */
}

/* Flexbox voor titel en tekst naast elkaar */
.text-container h1 {
  margin-top: 0; /* Verwijder de margin-top om de titel naar boven te krijgen */
  margin-right: 10px; /* Zorg ervoor dat er ruimte is tussen de titel en de tekst */
  flex: 0 0 auto; /* Zorg ervoor dat de titel niet uitrekt */
}

/* Rest van de tekst container */
.text-content {
  padding-left: 10px; /* Voeg ruimte toe aan de linkerzijde van de tekst */
  flex-grow: 1; /* Laat de tekstcontainer de beschikbare ruimte opvullen */
}

/* Aanpassen van de styling voor de tekst */
.text-3xl {
  font-family: "Epilogue", sans-serif;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  color: crimson;
  font-size: 50pt;
}
</style>

<script setup>
defineProps(['data', 'formatDate']);
</script>



  