<template>
  <!-- SEARCH -->
  <div :class="$q.screen.gt.md ? 'q-ml-xl ' : ''">
    <div class="row rounded-borders q-pa-md justify-center">
      <q-expansion-item
        class="shadow-1 overflow-hidden bg-primary"
        :class="!store.components.state.leftDrawerOpen ? 'z-top' : ''"
        style="border-radius: 30px; width: 80vh"
        :style="
          $q.screen.lt.md && !store.components.state.searchBoxClicked
            ? 'width:100%;'
            : ''
        "
        icon="people"
        label="Praktek Dokter Hari Ini"
        header-class="text-accent text-h6"
        expand-icon-class="text-grey-10"
        expand-icon="search"
        expanded-icon="close"
        @show="atShow"
        @hide="atHide"
      >
        <!-- <q-scroll-observer @scroll="showScrollGuide = true" /> -->
        <!-- <template v-slot:header>
        
        <div class="text-subtitle2">
          <q-icon size="40px" name="people" color="grey-8"/>
          Praktek Dokter Hari Ini
          <q-space />
          </div>
      </template> -->
        <q-card>
          <q-card-section>
            <!-- search -->
            <q-input
              ref="input"
              v-model="store.doctor.state.searchSpecialist.value"
              autofocus
              class="q-mr-md"
              dense
              outlined
              rounded
              placeholder="Ketik   Nama Dokter / Poli"
            >
              <template #prepend>
                <q-icon
                  v-if="store.doctor.state.searchText.value === ''"
                  name="search"
                />
                <!-- <q-icon v-else name="clear" class="cursor-pointer" @click="search = ''" /> -->
              </template>
            </q-input>
          </q-card-section>
        </q-card>
      </q-expansion-item>
    </div>
  </div>
</template>

<script>
import { inject, nextTick, ref, onMounted } from "vue";
export default {
  setup() {
    const store = inject("store");
    const input = ref(null);
    const atShow = () => {
      nextTick(() => {
        input.value.focus();
      });
      store.components.state.searchBoxClicked = true;
    };
    const atHide = () => {
      store.doctor.state.searchText.value = "";
      store.components.state.searchBoxClicked = false;
    };

    return {
      store,
      atShow,
      atHide,
      input,
    };
  },
};
</script>

<style></style>
