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
      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">My TodoList</div>
        <div class="text-subtitle">{{ currentDate() }}</div>
      </div>
      <q-img class="header-image absolute-top" src="../assets/2.png" />
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="250"
      :breakpoint="600"
    >
      <q-scroll-area
        style="
          height: calc(100% - 185px);
          margin-top: 185px;
          border-right: 1px solid #ddd;
        "
      >
        <q-list padding>
          <q-item to="/" axact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section> Todo </q-item-section>
          </q-item>

          <q-item to="/helppage" axact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section> Help </q-item-section>
          </q-item>

          <q-item to="/aboutpage" axact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="link" />
            </q-item-section>

            <q-item-section> About </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img class="absolute-top image" style="height: 185px">
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="../assets/NadiaGallini.jpg" />
          </q-avatar>
          <div class="text-weight-bold">Надежда Галлини</div>
          <div>@nadia_gallini</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
      <q-footer class="my_footer">
        <a
          href="https://vk.com/nadia.gallini"
          target="_blank"
          class="social-link"
        >
          <i class="fab fa-vk"></i> ВКонтакте
        </a>
        <a href="mailto:gallininadia@gmail.com" class="social-link">
      <i class="far fa-envelope"></i> gallininadia@gmail.com
    </a>
        <!-- <q-btn
          round
          color="deep"
          style="background-color: #a5d6a7"
          icon="edit_location"
        /> -->
      </q-footer>
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";

defineOptions({
  name: "MainLayout",
});

const linksList = [
  {
    title: "Docs",
    caption: "quasar.dev",
    icon: "school",
    link: "https://quasar.dev",
  },
  {
    title: "Github",
    caption: "github.com/quasarframework",
    icon: "code",
    link: "https://github.com/quasarframework",
  },
  {
    title: "Discord Chat Channel",
    caption: "chat.quasar.dev",
    icon: "chat",
    link: "https://chat.quasar.dev",
  },
  {
    title: "Forum",
    caption: "forum.quasar.dev",
    icon: "record_voice_over",
    link: "https://forum.quasar.dev",
  },
  {
    title: "Twitter",
    caption: "@quasarframework",
    icon: "rss_feed",
    link: "https://twitter.quasar.dev",
  },
  {
    title: "Facebook",
    caption: "@QuasarFramework",
    icon: "public",
    link: "https://facebook.quasar.dev",
  },
  {
    title: "Quasar Awesome",
    caption: "Community Quasar projects",
    icon: "favorite",
    link: "https://awesome.quasar.dev",
  },
];

const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}

const currentDate = () => {
  const dateObj = new Date();
  const options = { year: "numeric", month: "long", day: "numeric" };
  return dateObj.toLocaleDateString("ru-RU", options);
};
</script>

<style lang="scss">
.header-image {
  height: 200px;
  z-index: -1;
  // width:200px;
  // margin:20px;
  // filter:rgb(232, 225, 225);
  opacity: 0.1;
}

.image {
  background-color: $primary;
}

.my_footer {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: $primary;
  color: white;
  padding: 10px 10px;
  text-align: center;
  display: flex;
  justify-content: center;
}

.social-link {
  color: #f9fafb; /* Цвет ссылки (цвет ВКонтакте) */
  text-decoration: none; /* Удаление подчеркивания */
  margin-right: 20px; /* Отступ справа */
}

.social-link:hover {
  color: #43648c; /* Изменение цвета при наведении */
}
</style>
