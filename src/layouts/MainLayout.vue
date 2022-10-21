<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          БГПУ
        </q-toolbar-title>

        <div>СЦОС</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label
          header
        >
          Основные разделы
        </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Образовательные',
    caption: 'программы',
    icon: 'school',
    link: '/education'
  },
  {
    title: 'Учебные',
    caption: 'планы',
    icon: 'code',
    // link: 'https://github.com/quasarframework'
  },
  {
    title: 'Дисциплины',
    // caption: 'chat.quasar.dev',
    icon: 'chat',
    // link: 'https://chat.quasar.dev'
  },
  {
    title: 'Студенты',
    // caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    // link: 'https://forum.quasar.dev'
  },
  {
    title: 'Движение',
    caption: 'контингента',
    icon: 'rss_feed',
    // link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Оценки',
    // caption: '@QuasarFramework',
    icon: 'public',
    // link: 'https://facebook.quasar.dev'
  },
]

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>
