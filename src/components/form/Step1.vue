<template>
  <div class="col-md-3">
    <div class="row no-wrap items-center">
      <!-- Dokter -->
      <transition
        v-if="showCard"
        appear
        enter-active-class="animated fadeInLeft"
        leave-active-class="animated fadeOut"
      >
        <q-card
          flat
          class="transparent q-mt-sm q-pa-sm"
          style="
            border-radius: 30px;
            height: 270px;
            border-right: 1px solid grey;
          "
        >
          <div class="row no-wrap" style="margin-bottom: -15px">
            <q-chip color="secondary" text-color="white">
              <q-avatar color="primary" text-color="accent"
                ><strong>1</strong></q-avatar
              >
              Dokter Tujuan
            </q-chip>
            <q-space />
            <router-link to="/doctor/search" style="text-decoration: none">
              <q-chip
                v-if="$route.params.id"
                icon="swap_horiz"
                size="xs"
                class="shadow-2 cursor-pointer"
                rounded
                color="primary"
                text-color="accent"
              >
                Ganti Dokter
              </q-chip>
            </router-link>
          </div>
          <!-- :picture-url="store.doctor.state.selected().url" -->
          <card-doctor
            v-if="$route.params.id"
            :doctor="store.doctor.state.selected.nama"
            :specialist="store.doctor.state.selected.specialist"
            :time="store.doctor.state.selected.time"
          />
          <q-card-section
            v-if="!$route.params.id"
            class="row items-center justify-center q-mt-xl"
          >
            <router-link to="/doctor/search" style="text-decoration: none">
              <q-btn
                class="text-primary bg-white"
                style="border-radius: 30px"
                @click="
                  store.doctor.state.searchDate.value =
                    store.components.state.today()
                "
              >
                Pilih Dokter
              </q-btn>
            </router-link>
          </q-card-section>
        </q-card>
      </transition>
    </div>
  </div>
</template>

<script>
import { inject, ref, onMounted} from "vue";
import CardDoctor from "../CardDoctor.vue";
import { useRouter } from 'vue-router';
import { useQuasar } from 'quasar';

export default {
  components: {
    CardDoctor,
  },
  setup() {
    const store = inject("store");
    const $q = useQuasar()
    const router = useRouter()
    const showCard = ref(false);
    setTimeout(() => {
      showCard.value = true;
    }, 100);
    const showNext = ref(false);
    setTimeout(() => {
      showNext.value = true;
    }, 500);

    onMounted(()=>{
      // console.log(router);
      // console.log(Object.keys(store.doctor.state.selected).length == 0);
      if(Object.keys(store.doctor.state.selected).length == 0){
        router.push('/registration')
      }
    })
    return {
      store,
      showCard,
    };
  },
};
</script>

<style></style>
