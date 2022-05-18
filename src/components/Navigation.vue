<script setup>
import { RouterLink } from 'vue-router'

const navList = [
  {
    uid: '12343dfgg2',
    link: '/',
    label: 'Home'
  },
  {
    uid: '546fdgh777',
    link: '/about',
    label: 'About'
  },
  {
    uid: 'w3t4w3443',
    link: '/services',
    label: 'Services',
    nestedRoutes: [
      {
        uid: 'fdsg3wq45t',
        link: '/services/customer',
        label: 'Customers'
      },
      {
        uid: 'g3464gjh7n74',
        link: '/services/business',
        label: 'Businesses'
      }
    ]
  },
  {
    uid: '4567sdfgff',
    url: 'https://vuejs.org',
    label: 'Vue docs'
  }
]
</script>

<template>
  <nav class="navigation">
    <ul>
      <li v-for="item in navList" :key="item.uid" class="group">
        <!-- main Links -->
        <RouterLink v-if="item.link" :to="item.link" class="linkStyling">
          {{ item.label }}
        </RouterLink>
        <a
          v-else-if="item.url"
          class="linkStyling"
          :href="item.url"
          target="_blank"
        >
          {{ item.label }}
        </a>

        <!-- nested links in dropdown -->
        <div class="dropdown" v-if="item.nestedRoutes">
          <ul>
            <li v-for="nestedLink in item.nestedRoutes" :key="nestedLink.uid">
              <RouterLink
                v-if="nestedLink.link"
                :to="nestedLink.link"
                class="linkStyling"
              >
                {{ nestedLink.label }}
              </RouterLink>
              <a
                v-else-if="nestedLink.url"
                class="linkStyling"
                :href="nestedLink.url"
                target="_blank"
              >
                {{ nestedLink.label }}
              </a>
            </li>
          </ul>
        </div>
      </li>
    </ul>
  </nav>
</template>

<style lang="postcss" scoped>
.navigation {
  @apply fixed bg-green-400 left-0 -top-10 text-white z-50;
}

.navigation > ul {
  @apply flex max-w-lg mx-auto py-10 md:py-8 gap-x-10 justify-around text-center;
}

.dropdown a {
  @apply text-white opacity-0 h-0 group-hover:opacity-100 group-hover:h-auto transition-all ease-in-out duration-500;
}

.linkStyling {
  @apply hover:underline;
}
</style>
