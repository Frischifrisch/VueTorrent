<template>
  <v-dialog
    v-model="dialog"
    scrollable
    content-class="rounded-form"
    max-width="500px"
  >
    <v-card>
      <v-card-title class="justify-center primarytext--text">
        <h2>Sort Torrents</h2>
      </v-card-title>
      <v-card-text>
        <v-form class="px-6 mt-3 justify-center mx-auto">
          <v-container class="sortmodal">
            <v-select
              v-model="sort_options.sort"
              :value="sortProperty"
              flat
              class="ml-2 mr-2"
              :items="options"
              item-text="name"
              item-value="value"
              dense
              solo
              height="55"
            />
            <v-switch
              v-model="sort_options.reverse"
              class="v-input--reverse v-input--expand pa-0 ma-0"
              inset
              color="accent"
              style="padding-left: 10px !important"
            >
              <template #label>
                Reverse
              </template>
            </v-switch>
          </v-container>
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
import { mapState } from 'vuex'
import { Modal } from '@/mixins'
export default {
  name: 'Sort',
  mixins: [Modal],
  data() {
    return {
      sortProperty: { value: 'added_on', name: 'Added On' },
      reverse: true,
      options: [
        { value: 'added_on', name: 'Added On' },
        { value: 'availability', name: 'Availability' },
        { value: 'category', name: 'Category' },
        { value: 'completed', name: 'Completed' },
        { value: 'dlspeed', name: 'Download Speed' },
        { value: 'downloaded', name: 'Downloaded' },
        { value: 'eta', name: 'ETA' },
        { value: 'name', name: 'Name' },
        { value: 'num_leechs', name: 'Peers' },
        { value: 'priority', name: 'Priority' },
        { value: 'progress', name: 'Progress' },
        { value: 'ratio', name: 'Ratio' },
        { value: 'size', name: 'Size' },
        { value: 'state', name: 'State' },
        { value: 'time_active', name: 'Time Active' },
        { value: 'uploaded', name: 'Uploaded' },
        { value: 'upspeed', name: 'Upload Speed' }
      ]
    }
  },
  computed: {
    ...mapState(['sort_options'])
  },
  methods: {
    close() {
      this.dialog = false
    }
  }
}
</script>

<style lang="scss" scoped>
.sortmodal .v-select__selection,
.v-input__icon i {
    color: var(--search) !important;
}
// Reversed input variant
::v-deep .v-input--reverse .v-input__slot {
  @import "src/styles/styles.scss";
  @include reverse-switch;
}
</style>
