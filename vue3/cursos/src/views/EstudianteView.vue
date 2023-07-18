<template>
  <div>
  <Tabs>
    <slot></slot>
    <template v-slot:lista>Contenido de Listar</template>
    <template v-slot:nuevo>Nuevo Estudiante</template>
  </Tabs>
  </div>
</template>

<script>
// @ is an alias to /src
import Tabs from '@/components/Tabs.vue'

export default {
  name: 'Estudiante',
  components: {
    Tabs
  }
}
</script>
