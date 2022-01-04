<template>
  <q-layout view="lHr lpr lFr">

    <q-header elevated class="bg-light-blue-13 text-white" height-hint="98">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title>

            <q-icon size="xl" name="sports_esports" />

          Game-UI
        </q-toolbar-title>

        <q-btn dense flat round icon="menu" @click="toggleRightDrawer" />
      </q-toolbar>

    </q-header>

    <q-drawer show-if-above v-model="leftDrawerOpen" side="left" bordered>
      <q-scroll-area class="fit">
          <q-list>

            <template v-for="(menuItem, index) in menuList" :key="index">
              <q-item @click="showLoading" clickable :active="menuItem.label === 'Outbox'" v-ripple>
                <q-item-section avatar>
                  <q-icon :name="menuItem.icon" />
                </q-item-section>
                <q-item-section>
                  {{ menuItem.label }}
                </q-item-section>
              </q-item>
              <q-separator :key="'sep' + index"  v-if="menuItem.separator" />
            </template>

          </q-list>
        </q-scroll-area>
    </q-drawer>

    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <div class="q-pa-md text-body text-grey text-justify">
        Cuenta estes en algun juego o pregunta, se activara esta seccion
      </div>
      <q-icon style="font-size: 50vw;" color="grey" name="sentiment_very_satisfied" class="absolute-center"/>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer elevated class="bg-pink-13 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <div class="text-caption">Informacion del Sistema de Juego</div>
        </q-toolbar-title>
        <div class="text-caption">
          Hora del servidor: 12:00:00
        </div>
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>

<script>
import { ref } from 'vue'
import { useQuasar, QSpinnerPie } from 'quasar'
import { onBeforeUnmount } from 'vue'
export default {
  setup () {
    const $q = useQuasar()
    let timer

    onBeforeUnmount(() => {
      if (timer !== void 0) {
        clearTimeout(timer)
        $q.loading.hide()
      }
    })
    const menuList = [
  {
    icon: 'map',
    label: 'Mapa',
    separator: false
  },
  {
    icon: 'account_circle',
    label: 'Cuenta',
    separator: false
  },
  {
    icon: 'help',
    label: 'Ayuda',
    separator: true
  },
  {
    icon: 'logout',
    label: 'Cerrar Sesion',
    separator: false
  }
]

    const leftDrawerOpen = ref(false)
    const rightDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },

      rightDrawerOpen,
      toggleRightDrawer () {
        rightDrawerOpen.value = !rightDrawerOpen.value
      },
      menuList,
      showLoading () {
        $q.loading.show({
          spinner: QSpinnerPie,
          spinnerColor: 'white',
          spinnerSize: 100,
          backgroundColor: 'blue-12',
          message: 'Cargando datos un momento por favor...',
          messageColor: 'white'
        })

        // hiding in 3s
        timer = setTimeout(() => {
          $q.loading.hide()
          timer = void 0
        }, 3000)
      }
    }
  }
}
</script>