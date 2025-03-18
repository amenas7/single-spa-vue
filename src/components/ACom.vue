<template>
  <h2 class="vue-title"> <span>Hola desde vue</span> <img class="img_loco_vue" src="logo.png" alt=""></h2>
  <div>
    <page-header title="Generador de imágenes"></page-header>
    <div class="content">
      <div class="card">
        <div v-if="isLoading" class="spinner-container">
          <div class="spinner"></div>
          <p style="color: #41B883;">Cargando imagen...</p>
        </div>
        <div v-else-if="currentImageUrl" class="image-container">
          <img :src="currentImageUrl" alt="random image" class="img-fluid fade-in" />
        </div>
        <div class="actions">
          <button @click="generateNewImage" class="btn generate-btn" :class="{ 'active': isButtonActive }">Generar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: () => ({
    currentImageUrl: null,
    isLoading: false,
    isButtonActive: false
  }),
  created() {
    // Agregar Bootstrap CSS
    if (!document.getElementById('bootstrap-css')) {
      const link = document.createElement('link');
      link.id = 'bootstrap-css';
      link.rel = 'stylesheet';
      link.href = 'https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css';
      link.integrity = 'sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN';
      link.crossOrigin = 'anonymous';
      document.head.appendChild(link);
    }
    
    // Agregar Bootstrap JS
    if (!document.getElementById('bootstrap-js')) {
      const script = document.createElement('script');
      script.id = 'bootstrap-js';
      script.src = 'https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js';
      script.integrity = 'sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL';
      script.crossOrigin = 'anonymous';
      script.defer = true;
      document.body.appendChild(script);
    }
    
    this.generateNewImage();
  },
  methods: {
    generateNewImage() {
      this.isLoading = true;
      this.currentImageUrl = null;
      
      // Efecto visual para el botón
      this.isButtonActive = true;
      setTimeout(() => {
        this.isButtonActive = false;
      }, 300);
      
      // Simulamos un pequeño retraso para ver el spinner
      setTimeout(() => {
        // Añadimos un timestamp para evitar caché
        this.currentImageUrl = `https://picsum.photos/200/300?random=${Date.now()}`;
        
        // Creamos un objeto Image para detectar cuando la imagen ha cargado
        const img = new Image();
        img.onload = () => {
          this.isLoading = false;
        };
        img.src = this.currentImageUrl;
      }, 500);
    }
  }
}
</script>

<style scoped>

.card{
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  border: none;
}

span {
  color: #41B883
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.vue-title{
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.img_loco_vue{
  width: 5%;
}

.content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.card {
  margin-top: 1.6rem;
  padding: 3.2rem;
  background-color: white;
  border-radius: 0.5rem;
  width: 300px;
  height: 450px; /* Fixed height instead of min-height */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
  overflow: hidden; /* Prevent content from overflowing */
}

.card img {
  max-width: 100%;
  height: 300px; /* Fixed height for the image */
  object-fit: contain;
}

.spinner-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 300px; /* Match the image height */
  width: 100%;
}

.actions {
  margin-top: 1.6rem;
  display: flex;
  justify-content: center;
}

.generate-btn {
  color: white;
  border: none;
  background-color: #41B883;
  transition: all 0.3s ease;
}

.generate-btn:hover {
  color: white;
  background-color: #41B883;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.generate-btn.active {
  color: white;
  transform: scale(0.95);
}

.spinner-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 300px;
}

.spinner {
  border: 4px solid rgba(0, 0, 0, 0.1);
  width: 36px;
  height: 36px;
  border-radius: 50%;
  border-left-color: #42b983;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.image-container {
  width: 100%;
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.fade-in {
  animation: fadeIn 0.5s ease-in;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
