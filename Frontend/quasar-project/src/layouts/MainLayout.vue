<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="custom-header">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title class="text-center-h1 custom-title">Knjižnica</q-toolbar-title>


        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label header>
          Essential Links
        </q-item-label>

        <q-item
          v-for="link in linksList"
          :key="link.title"
          clickable
          @click="navigateTo(link.link)"
        >
          <q-item-section avatar>
            <q-icon :name="link.icon" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{ link.title }}</q-item-label>
            <q-item-label caption>{{ link.caption }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

defineOptions({
  name: 'MainLayout'
});

const linksList = [
  { title: 'Početna', caption: 'Početna stranica', icon: 'home', link: '/' },
  { title: 'Popis knjiga', caption: 'Popis svih knjiga u knjižnici', icon: 'book', link: '/popisKnjiga' },
  { title: 'Pretraživanje', caption: 'Tražiš knjigu?', icon: 'search', link: '/Pretrazivanje' },
  { title: 'Rezervirane knjige', caption: 'Rezerviranje knjige', icon: 'book', link: '/Rezervacija' },
  { title: 'O nama', caption: 'o_nama', icon: 'record_voice_over', link: '/O_nama' },
  { title: 'Lokacija', caption: 'Gdje se nalazimo?', icon: 'pin_drop', link: '/Lokacija' },
  { title: 'Login', caption: 'Prijava korisnika', icon: 'login', link: '/Login' },
  { title: 'Registracija', caption: 'Registracija korisnika', icon: 'app_registration', link: '/Registracija' },
  { title: 'Popis knjiga - baza', caption: 'Baza knjiga', icon: 'book', link: '/PopisKnjigaBaza' }
]

const leftDrawerOpen = ref(false);
const router = useRouter();

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}

function navigateTo(route) {
  router.push(route);
}
</script>

<style scoped>
.custom-header {
  background-color: #fce4ec;
  color: white;
}

.custom-title {
  font-weight: bold;
  font-size: 2.5em;
  text-transform: uppercase;
  color: #ffffff;
}
</style>

