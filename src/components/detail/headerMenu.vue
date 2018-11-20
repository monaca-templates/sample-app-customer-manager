<template>
  <v-menu v-model="menuOpened" bottom offset-y>
    <v-btn slot="activator" class="header-icon" icon>
      <v-icon>more_vert</v-icon>
    </v-btn>
    <v-list>
      <v-list-tile @click="$emit('on-click-edit')">
        <v-list-tile-title>
          <v-icon>edit</v-icon>
          {{ $t('common.edit') }}
        </v-list-tile-title>
      </v-list-tile>
        <ConfirmDialog
          :rendered="deleteConfirmDialogRendered"
          :title="$t('confirm.delete_title')"
          :message="$t('confirm.delete_message')"
          @on-accept="onAccept"
          @on-reject="onReject"
        >
          <v-list-tile slot="button" @click="renderDeleteConfirmDialog">
            <v-list-tile-title>
              <v-icon>delete</v-icon>
              {{ $t('common.delete') }}
            </v-list-tile-title>
          </v-list-tile>
        </ConfirmDialog>
    </v-list>
  </v-menu>
</template>

<script>
  import ConfirmDialog from '../common/ConfirmDialog'

  export default {
    name: 'HeaderMenu',
    components: {
      ConfirmDialog,
    },
    data: () => {
      return {
        menuOpened: false,
        deleteConfirmDialogRendered: false,
      }
    },
    methods: {
      renderDeleteConfirmDialog () {
        this.deleteConfirmDialogRendered = true
        this.menuOpened = false
      },
      onAccept () {
        this.deleteConfirmDialogRendered = false
        this.$emit('on-click-delete')
      },
      onReject () {
        this.deleteConfirmDialogRendered = false
      }
    }
  }
</script>
