<template>
  <v-container class="fill-height">
    <v-responsive class="d-flex align-center text-center fill-height">
      <v-img contain height="300" src="@/assets/logo.svg" />
      <div class="text-body-2 font-weight-light mb-n1">Welcome to</div>
      <h1 class="text-h2 font-weight-bold">Vuetify</h1>
      <div class="py-14" />
      <v-row class="d-flex align-center justify-center">
        <v-col cols="auto">
          <v-btn href="https://next.vuetifyjs.com/components/all/" min-width="164" rel="noopener noreferrer"
            target="_blank" variant="text">
            <v-icon icon="mdi-view-dashboard" size="large" start />

            Components
          </v-btn>
        </v-col>
        <v-col cols="auto">
          <v-btn to="/login" color="primary" min-width="228" size="x-large" variant="flat">
            <v-icon icon="mdi-speedometer" size="large" start />

            Get Started
          </v-btn>
        </v-col>
        <v-col cols="auto">
          <v-btn href="https://community.vuetifyjs.com/" min-width="164" rel="noopener noreferrer" target="_blank"
            variant="text">
            <v-icon icon="mdi-account-group" size="large" start />

            Community
          </v-btn>
        </v-col>
      </v-row>
    </v-responsive>
  </v-container>
</template>

<script setup>
  //
</script>
