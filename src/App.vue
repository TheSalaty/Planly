<script setup lang="ts">
// https://github.com/vueuse/head
// you can use this to manipulate the document head in any components,
// they will be rendered correctly in the html results with vite-ssg
import { CheckIcon, ThumbUpIcon, UserIcon } from '@heroicons/vue/solid'
import { isDark, preferredDark } from '~/composables'

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

const tabs = [
  { name: 'Kalender', href: '/kalender', current: false },
  { name: 'Tasks', href: '/tasks', current: true },
  { name: 'E-Kacheln', href: '/e-kachel', current: false },
]

const timeline = [
  {
    id: 1,
    content: 'Applied to',
    target: 'Front End Developer',
    href: '#',
    date: 'Sep 20',
    datetime: '2020-09-20',
    icon: UserIcon,
    iconBackground: 'bg-gray-400',
  },
  {
    id: 2,
    content: 'Advanced to phone screening by',
    target: 'Bethany Blake',
    href: '#',
    date: 'Sep 22',
    datetime: '2020-09-22',
    icon: ThumbUpIcon,
    iconBackground: 'bg-blue-500',
  },
  {
    id: 3,
    content: 'Completed phone screening with',
    target: 'Martha Gardner',
    href: '#',
    date: 'Sep 28',
    datetime: '2020-09-28',
    icon: CheckIcon,
    iconBackground: 'bg-green-500',
  },
  {
    id: 4,
    content: 'Advanced to interview by',
    target: 'Bethany Blake',
    href: '#',
    date: 'Sep 30',
    datetime: '2020-09-30',
    icon: ThumbUpIcon,
    iconBackground: 'bg-blue-500',
  },
  {
    id: 5,
    content: 'Completed interview with',
    target: 'Katherine Snyder',
    href: '#',
    date: 'Oct 4',
    datetime: '2020-10-04',
    icon: CheckIcon,
    iconBackground: 'bg-green-500',
  },
]
</script>

<template>
  <div class="flex flex-row h-25">
    <img class="m-2" src="https://placekeanu.com/100/100" alt="">
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
          <a
            v-for="(tab, tabIdx) in tabs" :key="tab.name" :href="tab.href"
            class="group relative min-w-0 flex-1 overflow-hidden bg-white py-4 px-4 text-sm font-medium text-center hover:bg-gray-50 focus:z-10"
            :class="[tab.current ? 'text-gray-900' : 'text-gray-500 hover:text-gray-700', tabIdx === 0 ? 'rounded-l-lg' : '', tabIdx === tabs.length - 1 ? 'rounded-r-lg' : '']"
            :aria-current="tab.current ? 'page' : undefined"
          >
            <span>{{ tab.name }}</span>
            <span
              aria-hidden="true" class="absolute inset-x-0 bottom-0 h-0.5"
              :class="[tab.current ? 'bg-indigo-500' : 'bg-transparent']"
            />
          </a>
        </nav>
      </div>
    </div>
    <img src="https://placekeanu.com/90/90" class="rounded-full m-2" alt="">
  </div>
  <div class="flex flex-row w-full">
    <div w-50>
      <div class="flow-root">
        <ul role="list" class="-mb-8">
          <li v-for="(event, eventIdx) in timeline" :key="event.id">
            <div class="relative pb-8">
              <span v-if="eventIdx !== timeline.length - 1" class="absolute top-4 left-4 -ml-px h-full w-0.5 bg-gray-200" aria-hidden="true" />
              <div class="relative flex space-x-3">
                <div>
                  <span class="h-8 w-8 rounded-full flex items-center justify-center ring-8 ring-white" :class="[event.iconBackground]">
                    <component :is="event.icon" class="h-5 w-5 text-white" aria-hidden="true" />
                  </span>
                </div>
                <div class="min-w-0 flex-1 pt-1.5 flex justify-between space-x-4">
                  <div>
                    <p class="text-sm text-gray-500">
                      {{ event.content }} <a :href="event.href" class="font-medium text-gray-900">{{ event.target }}</a>
                    </p>
                  </div>
                  <div class="text-right text-sm whitespace-nowrap text-gray-500">
                    <time :datetime="event.datetime">{{ event.date }}</time>
                  </div>
                </div>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <div class="w-full">
      <RouterView />
    </div>
  </div>
</template>
