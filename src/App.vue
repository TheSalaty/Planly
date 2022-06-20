<script setup lang="ts">
// https://github.com/vueuse/head
// you can use this to manipulate the document head in any components,
// they will be rendered correctly in the html results with vite-ssg
import TaskCard from './components/TaskCard.vue'
import { isDark, preferredDark } from '~/composables'

const router = useRouter()

useHead({
  title: 'Vitesse',
  meta: [
    { name: 'description', content: 'Opinionated Vite Starter Template' },
    {
      name: 'theme-color',
      content: computed(() => isDark.value ? '#00aba9' : '#ffffff'),
    },
  ],
  link: [
    {
      rel: 'icon',
      type: 'image/svg+xml',
      href: computed(() => preferredDark.value ? '/favicon-dark.svg' : '/favicon.svg'),
    },
  ],
})

const tabs = computed(() => {
  const path = router.currentRoute.value.fullPath

  return [
    { name: 'Kalender', href: '/kalender', current: path === '/kalender' },
    { name: 'Tasks', href: '/tasks', current: path === '/tasks' },
    { name: 'E-Kacheln', href: '/e-kachel', current: path === '/e-kachel' },
  ]
},
)

const tasks = [
  {
    id: 6,
    title: 'Design shopping cart dropdown',
    date: 'Sep 9',
    type: 'Design',
  },
  {
    id: 7,
    title: 'Add discount code to checkout page',
    date: 'Sep 14',
    type: 'Feature Request',
  },
  {
    id: 8,
    title: 'Provide documentation on integrations',
    date: 'Sep 12',
    type: 'Backend',
  },
]
</script>

<template>
  <div class="flex flex-row h-25">
    <img class="m-2" src="planly.png" alt="">
    <div class="w-full">
      <div class="sm:hidden">
        <label for="tabs" class="sr-only">Select a tab</label>
        <!-- Use an "onChange" listener to redirect the user to the selected tab URL. -->
        <select
          id="tabs" name="tabs"
          class="block w-full focus:ring-indigo-500 focus:border-indigo-500 border-gray-300 rounded-md"
        >
          <option v-for="tab in tabs" :key="tab.name" :selected="tab.current">
            {{ tab.name }}
          </option>
        </select>
      </div>
      <div class="hidden sm:block">
        <nav class="relative z-0 rounded-lg shadow flex divide-x divide-gray-200" aria-label="Tabs">
          <router-link
            v-for="(tab, tabIdx) in tabs" :key="tab.name" :to="tab.href"
            class="group relative min-w-0 flex-1 overflow-hidden bg-white py-4 px-4 text-sm font-medium text-center hover:bg-gray-50 focus:z-10"
            :class="[tab.current ? 'text-gray-900' : 'text-gray-500 hover:text-gray-700', tabIdx === 0 ? 'rounded-l-lg' : '', tabIdx === tabs.length - 1 ? 'rounded-r-lg' : '']"
            :aria-current="tab.current ? 'page' : undefined"
          >
            <span>{{ tab.name }}</span>
            <span
              aria-hidden="true" class="absolute inset-x-0 bottom-0 h-0.5"
              :class="[tab.current ? 'bg-indigo-500' : 'bg-transparent']"
            />
          </router-link>
        </nav>
      </div>
    </div>
    <img src="https://placekeanu.com/90/90" class="rounded-full m-2" alt="">
  </div>
  <div class="flex flex-row w-full">
    <div class="w-60 mx-5">
      <div class="flow-root">
        <task-card
          v-for="task in tasks"
          :key="task.id"
          :task="task"
          class="mt-3 cursor-move  shadow-md w-full"
        />
      </div>
    </div>
    <div class="w-full">
      <RouterView />
    </div>
  </div>
</template>
