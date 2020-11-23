<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />
      </q-toolbar>
      <div class="q-px-sm q-pt-sm q-mb-sm">
        <div class="text-h3">TareaX</div>
        <div class="text-subtitle1">{{todaysDate}}</div>
      </div>
    </q-header>

    <q-drawer v-model="leftDrawerOpen">
        <q-scroll-area class="fit">
          <q-list padding class="menu-list">
            <q-item 
              to="/tarea"
              exact
              clickable 
              v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Tareas
              </q-item-section>
            </q-item>

            <q-item 
              to="/acerca"
              exact
              clickable 
              v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Acerca 
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>
      </q-drawer>

      <q-footer elevated>
        <q-toolbar>
          <q-toolbar-title>Desarrollado por Nahuel Jurado</q-toolbar-title>
        </q-toolbar>
      </q-footer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive> 
    </q-page-container>
  </q-layout>
</template>

<script>

import { date } from 'quasar'

export default {
  name: 'MainLayout',

  data () {
    return {
      leftDrawerOpen: false
    }
  },
  computed: {
    todaysDate(){
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM')
    }
  }
}
</script>
