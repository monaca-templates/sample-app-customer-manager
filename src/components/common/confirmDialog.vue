<template>
  <v-dialog v-model="rendered" persistent max-width="290">
    <slot slot="activator" name="button"></slot>
    <v-card>
      <v-card-title class="headline">{{ title }}</v-card-title>
      <v-card-text>{{ message }}</v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary" flat @click="$emit('on-accept')">{{ $t('confirm.accept') }}</v-btn>
        <v-btn color="primary" flat @click="$emit('on-reject')">{{ $t('confirm.reject') }}</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
  export default {
    name: 'ConfirmDialog',
    props: {
      rendered: Boolean,
      title: String,
      message: String,
    },
  }
</script>
