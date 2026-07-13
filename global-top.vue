<script setup lang="ts">
/**
 * global-top — camada renderizada ACIMA do conteúdo em todos os slides
 * (registrada automaticamente pelo Slidev por convenção de nome).
 *
 * Fornece uma barra inferior padronizada com o <Pager/> (página / total),
 * componente vindo do addon `slidev-component-pager`.
 *
 * Parametrização por slide (frontmatter):
 *   footer: false   -> oculta a barra neste slide
 * O padrão é EXIBIR a barra.
 */
import { useNav } from '@slidev/client'
import { computed } from 'vue'

const { currentSlideRoute } = useNav()

const frontmatter = computed(
  () => (currentSlideRoute.value.meta?.slide as any)?.frontmatter || {},
)

// Exibe por padrão; só oculta quando `footer: false` for definido no slide.
const showFooter = computed(() => frontmatter.value.footer !== false)
</script>

<template>
  <footer v-if="showFooter" class="slidev-footer">
    <div class="slidev-footer__end">
      <Pager />
    </div>
  </footer>
</template>

<style scoped>
.slidev-footer {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 1rem;
  padding: 0.4rem 1.25rem;
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  font-size: 0.78rem;
  line-height: 1;
  opacity: 0.75;
  z-index: 20;
  pointer-events: none;
}

.slidev-footer__end {
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
}

/* O <Pager/> do addon se posiciona sozinho (absolute, bottom/right).
   Aqui neutralizamos isso para ele fluir dentro da barra. */
.slidev-footer :deep(.pager) {
  position: static;
  padding: 0;
  font-size: inherit;
  line-height: inherit;
}
</style>
