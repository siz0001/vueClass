<template>
    <v-card>
        <v-card-title>
            login
        </v-card-title>
        <v-chip>
            {{x}}
        </v-chip>
        <v-chip>
            {{y}}
        </v-chip>
        <v-chip @click="isDark = !isDark">
            {{isDark}}
        </v-chip>
        <v-card-text>
            {{ store }}
        </v-card-text>
    </v-card>
</template>
  
<script setup>
import { useLocalStorage, useMouse, usePreferredDark } from '@vueuse/core'

const { x, y } = useMouse()

// is user prefers dark theme
const isDark = usePreferredDark()

// persist state in localStorage
const store = useLocalStorage(
  'my-storage',
  {
    name: 'Apple',
    color: 'red',
  },
)

</script>
  