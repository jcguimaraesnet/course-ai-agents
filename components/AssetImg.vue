<script setup lang="ts">
/**
 * AssetImg — <img> para arquivos da pasta `public/`, ciente do `base` do Vite.
 *
 * Por que existe:
 *   - `<img src="/foo.jpg">` (estático) quebra no build do Slidev (import guard / fs.allow).
 *   - `<img :src="'/foo.jpg'">` (runtime) funciona, mas NÃO recebe o prefixo do `--base`,
 *     então quebraria em produção num project site (ex.: /course-ai-agents/).
 *
 * Este componente resolve o caminho contra `import.meta.env.BASE_URL`:
 *   dev        -> BASE_URL = "/"                  -> /foo.jpg
 *   produção   -> BASE_URL = "/course-ai-agents/" -> /course-ai-agents/foo.jpg
 *
 * Uso:  <AssetImg src="foo.jpg" class="rounded-lg h-70" />
 */
import { computed } from 'vue'

const props = defineProps<{
  /** Caminho do arquivo dentro de `public/` (com ou sem "/" inicial). */
  src: string
  alt?: string
}>()

const resolved = computed(() => {
  const base = import.meta.env.BASE_URL || '/'
  return `${base.replace(/\/$/, '')}/${props.src.replace(/^\//, '')}`
})
</script>

<template>
  <img :src="resolved" :alt="alt ?? ''" />
</template>
