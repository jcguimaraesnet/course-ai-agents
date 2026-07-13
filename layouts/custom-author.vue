<script setup lang="ts">
/**
 * custom-author — layout de apresentação de pessoa/autor.
 *
 * Estrutura em duas colunas (inspirada no layout `about-me` do tema Mokkapps),
 * porém totalmente genérica via slots — cada parte do layout é um slot:
 *
 *   ::title::     título/nome        (coluna de conteúdo)
 *   ::subtitle::  subtítulo/cargo    (coluna de conteúdo)
 *   default       corpo/bullets      (coluna de conteúdo)
 *   ::image::     visual/foto        (coluna de imagem)
 *   ::links::     links/ações        (canto inferior direito)
 *
 * Por padrão a imagem fica à direita e o conteúdo à esquerda (como na referência).
 * Use a prop de frontmatter `imageSide: left` para inverter os lados.
 */
defineProps<{
  /** Lado onde a imagem é exibida: 'right' (padrão) ou 'left'. */
  imageSide?: 'left' | 'right'
}>()
</script>

<template>
  <div class="slidev-layout custom-author">
    <div
      class="ca-container"
      :class="imageSide === 'left' ? 'ca--image-left' : 'ca--image-right'"
    >
      <!-- Coluna de conteúdo -->
      <div class="ca-content">
        <div class="ca-title">
          <slot name="title" />
        </div>
        <div class="ca-subtitle">
          <slot name="subtitle" />
        </div>
        <div class="ca-body">
          <slot />
        </div>
      </div>

      <!-- Coluna de imagem -->
      <figure class="ca-image">
        <slot name="image" />
      </figure>
    </div>

    <!-- Links/ações no canto inferior direito -->
    <div v-if="$slots.links" class="ca-links">
      <slot name="links" />
    </div>
  </div>
</template>

<style scoped>
.custom-author {
  height: 100%;
  position: relative;
}

.ca-container {
  display: flex;
  align-items: center;
  height: 100%;
  gap: 2.5rem;
}

.ca--image-right {
  flex-direction: row;
}

.ca--image-left {
  flex-direction: row-reverse;
}

.ca-content {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  flex: 1 1 55%;
  min-width: 0;
}

/* Título: aplica-se ao h1 (ou similar) que o autor escrever no slot. */
.ca-title :deep(:is(h1, h2)) {
  font-size: 3rem;
  line-height: 1.1;
  margin: 0;
}

.ca-subtitle {
  font-size: 1.25rem;
  opacity: 0.85;
}

.ca-subtitle :deep(p) {
  margin: 0;
}

.ca-body :deep(ul) {
  line-height: 1.9;
  margin-top: 0.5rem;
}

/* Coluna de imagem */
.ca-image {
  flex: 1 1 45%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0;
}

/* Estilo padrão para uma <img> colocada no slot ::image::.
   O autor pode sobrescrever passando classes próprias na imagem. */
.ca-image :deep(img) {
  width: 20rem;
  height: 20rem;
  object-fit: cover;
  border-radius: 9999px;
  border: 6px solid var(--slidev-theme-primary, #bd93f9);
  z-index: 10;
}

/* Links/ações no canto inferior direito.
   Aceita vários links; cada parágrafo/linha fica um abaixo do outro. */
.ca-links {
  position: absolute;
  right: 15px;
  /* Acima da barra inferior global (global-top.vue) para não sobrepor. */
  bottom: 44px;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 0.25rem;
  font-size: 0.9rem;
  opacity: 0.9;
}

/* Cada linha de link é um wrapper (<div>/<p>): ícone + texto na mesma linha.
   Coloque cada link do slot ::links:: dentro do seu próprio elemento, ex.:
     <div><logos-linkedin-icon /> <a href="...">texto</a></div> */
.ca-links :deep(div),
.ca-links :deep(p) {
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 0.4rem;
  white-space: nowrap;
}

/* Normaliza o tamanho dos ícones (logos-*, GitHubIcon SVG, etc.). */
.ca-links :deep(svg),
.ca-links :deep(.iconify) {
  width: 1.1em;
  height: 1.1em;
  flex-shrink: 0;
}
</style>
