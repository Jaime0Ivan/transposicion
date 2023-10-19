<template>
  <div class="container mt-5">
    <h2 class="text-center mb-4">Cifrado y Descifrado de Transposición en Vue</h2>
    <div class="mb-3">
      <label for="texto" class="form-label">Texto:</label>
      <input type="text" class="form-control" v-model="texto" id="texto" />
    </div>
    <div class="mb-3">
      <label for="contraseña" class="form-label">Contraseña:</label>
      <input type="password" class="form-control" v-model="contraseña" id="contraseña" />
    </div>
    <button class="btn btn-secondary mr-4" @click="realizarCifrado">Cifrar</button>
    <button class="btn btn-primary" @click="realizarDescifrado">Descifrar</button>
    <div class="mb-3">
      <label class="form-label">Texto Cifrado:</label>
      <div class="form-control" readonly>{{ textoCifrado }}</div>
    </div>
    <div class="mb-3">
      <label class="form-label">Texto Descifrado:</label>
      <div class="form-control" readonly>{{ textoDescifrado }}</div>
    </div>
  </div>
</template>

<script>
import CryptoJS from "crypto-js";

export default {
  data() {
    return {
      texto: "",
      contraseña: "",
      textoCifrado: "",
      textoDescifrado: "",
    };
  },
  methods: {
    realizarCifrado() {
      if (this.texto && this.contraseña) {
        const textoCifrado = CryptoJS.AES.encrypt(this.texto, this.contraseña).toString();
        this.textoCifrado = textoCifrado;
      } else {
        alert("Por favor, ingresa texto y una contraseña.");
      }
    },
    realizarDescifrado() {
      if (this.textoCifrado && this.contraseña) {
        try {
          const bytes = CryptoJS.AES.decrypt(this.textoCifrado, this.contraseña);
          const textoOriginal = bytes.toString(CryptoJS.enc.Utf8);
          this.textoDescifrado = textoOriginal;
        } catch (error) {
          alert("No se pudo descifrar el texto. Verifica la contraseña.");
        }
      } else {
        alert("Por favor, ingresa texto cifrado y una contraseña.");
      }
    },
  },
};
</script>
