<template>
  <div class="h-screen flex overflow-hidden bg-gray-100">
    <!-- Off-canvas menu for mobile, show/hide based on off-canvas menu state. -->
    <transition name="mobile-navbar">
      <div
        v-show="showMobileNav"
        class="fixed inset-0 flex z-40 lg:hidden"
        role="dialog"
        aria-modal="true"
      >
        <!--
      Off-canvas menu overlay, show/hide based on off-canvas menu state.

      Entering: "transition-opacity ease-linear duration-300"
        From: "opacity-0"
        To: "opacity-100"
      Leaving: "transition-opacity ease-linear duration-300"
        From: "opacity-100"
        To: "opacity-0"
    -->
        <div
          class="fixed inset-0 bg-gray-600 bg-opacity-75"
          aria-hidden="true"
        ></div>

        <!--
      Off-canvas menu, show/hide based on off-canvas menu state.

      Entering: "transition ease-in-out duration-300 transform"
        From: "-translate-x-full"
        To: "translate-x-0"
      Leaving: "transition ease-in-out duration-300 transform"
        From: "translate-x-0"
        To: "-translate-x-full"
    -->
        <div
          class="
            relative
            flex-1 flex flex-col
            max-w-xs
            w-full
            pt-5
            pb-4
            bg-cyan-700
          "
        >
          <!--
        Close button, show/hide based on off-canvas menu state.

        Entering: "ease-in-out duration-300"
          From: "opacity-0"
          To: "opacity-100"
        Leaving: "ease-in-out duration-300"
          From: "opacity-100"
          To: "opacity-0"
      -->
          <div class="absolute top-0 right-0 -mr-12 pt-2">
            <button
              class="
                ml-1
                flex
                items-center
                justify-center
                h-10
                w-10
                rounded-full
                focus:outline-none
                focus:ring-2
                focus:ring-inset
                focus:ring-white
              "
              @click="showMobileNav = false"
            >
              <span class="sr-only">Close sidebar</span>
              <!-- Heroicon name: outline/x -->
              <svg
                class="h-6 w-6 text-white"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                aria-hidden="true"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M6 18L18 6M6 6l12 12"
                />
              </svg>
            </button>
          </div>

          <div class="flex-shrink-0 flex items-center px-4">
            <img
              class="h-8 w-auto"
              src="https://tailwindui.com/img/logos/easywire-logo-cyan-300-mark-white-text.svg"
              alt="Easywire logo"
            />
          </div>
          <nav
            class="
              mt-5
              flex-shrink-0
              h-full
              divide-y divide-cyan-800
              overflow-y-auto
            "
            aria-label="Sidebar"
          >
            <!-- List main menu for mobile -->
            <div class="px-2 space-y-1">
              <NuxtLink
                :to="{ name: 'admin' }"
                class="
                  text-cyan-100
                  hover:text-white hover:bg-cyan-600
                  group
                  flex
                  items-center
                  px-2
                  py-2
                  text-sm
                  leading-6
                  font-medium
                  rounded-md
                "
                aria-current="page"
              >
                <IconViewGrid class="size-2xl mr-4 text-cyan-200" />
                Thống kê
              </NuxtLink>

              <NuxtLink
                :to="{ name: 'admin-game' }"
                class="
                  text-cyan-100
                  hover:text-white hover:bg-cyan-600
                  group
                  flex
                  items-center
                  px-2
                  py-2
                  text-sm
                  leading-6
                  font-medium
                  rounded-md
                "
                aria-current="page"
              >
                <IconGamepad class="size-2xl mr-4 text-cyan-200" />
                Game
              </NuxtLink>

              <NuxtLink
                :to="{ name: 'admin-account' }"
                class="
                  text-cyan-100
                  hover:text-white hover:bg-cyan-600
                  group
                  flex
                  items-center
                  px-2
                  py-2
                  text-sm
                  leading-6
                  font-medium
                  rounded-md
                "
                aria-current="page"
              >
                <IconUserAlien class="size-2xl mr-4 text-cyan-200" />
                Account
              </NuxtLink>

              <NuxtLink
                :to="{ name: 'admin-recharge-phonecard' }"
                class="
                  text-cyan-100
                  hover:text-white hover:bg-cyan-600
                  group
                  flex
                  items-center
                  px-2
                  py-2
                  text-sm
                  leading-6
                  font-medium
                  rounded-md
                "
                aria-current="page"
              >
                <IconCreditCard class="size-2xl mr-4 text-cyan-200" />
                Recharge phonecard
              </NuxtLink>

              <NuxtLink
                :to="{ name: 'admin-coupon' }"
                class="
                  text-cyan-100
                  hover:text-white hover:bg-cyan-600
                  group
                  flex
                  items-center
                  px-2
                  py-2
                  text-sm
                  leading-6
                  font-medium
                  rounded-md
                "
                aria-current="page"
              >
                <IconTicket class="size-2xl mr-4 text-cyan-200" />
                Coupon
              </NuxtLink>
            </div>
            <div class="mt-6 pt-6">
              <div class="px-2 space-y-1">
                <NuxtLink
                  :to="{ name: 'admin-config' }"
                  class="
                    group
                    flex
                    items-center
                    px-2
                    py-2
                    text-base
                    font-medium
                    rounded-md
                    text-cyan-100
                    hover:text-white hover:bg-cyan-600
                  "
                >
                  <IconCog class="mr-4 h-6 w-6 text-cyan-200" />
                  Cấu hình
                </NuxtLink>

                <a
                  href="#"
                  class="
                    group
                    flex
                    items-center
                    px-2
                    py-2
                    text-base
                    font-medium
                    rounded-md
                    text-cyan-100
                    hover:text-white hover:bg-cyan-600
                  "
                >
                  <!-- Heroicon name: outline/question-mark-circle -->
                  <svg
                    class="mr-4 h-6 w-6 text-cyan-200"
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                    aria-hidden="true"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                    />
                  </svg>
                  Help
                </a>

                <a
                  href="#"
                  class="
                    group
                    flex
                    items-center
                    px-2
                    py-2
                    text-base
                    font-medium
                    rounded-md
                    text-cyan-100
                    hover:text-white hover:bg-cyan-600
                  "
                >
                  <!-- Heroicon name: outline/shield-check -->
                  <svg
                    class="mr-4 h-6 w-6 text-cyan-200"
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                    aria-hidden="true"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"
                    />
                  </svg>
                  Privacy
                </a>
              </div>
            </div>
          </nav>
        </div>

        <div class="flex-shrink-0 w-14" aria-hidden="true">
          <!-- Dummy element to force sidebar to shrink to fit close icon -->
        </div>
      </div>
    </transition>

    <!-- Static sidebar for desktop -->
    <div class="hidden lg:flex lg:flex-shrink-0">
      <div class="flex flex-col w-64">
        <!-- Sidebar component, swap this element with another sidebar if you like -->
        <div
          class="flex flex-col flex-grow bg-cyan-700 pt-5 pb-4 overflow-y-auto"
        >
          <div class="flex items-center flex-shrink-0 px-4">
            <img
              class="h-8 w-auto"
              src="https://tailwindui.com/img/logos/easywire-logo-cyan-300-mark-white-text.svg"
              alt="Easywire logo"
            />
          </div>
          <nav
            class="
              mt-5
              flex-1 flex flex-col
              divide-y divide-cyan-800
              overflow-y-auto
            "
            aria-label="Sidebar"
          >
            <!-- List main menu for desktop -->
            <div class="px-2 space-y-1">
              <NuxtLink
                :to="{ name: 'admin' }"
                class="
                  text-cyan-100
                  hover:text-white hover:bg-cyan-600
                  group
                  flex
                  items-center
                  px-2
                  py-2
                  text-sm
                  leading-6
                  font-medium
                  rounded-md
                "
                aria-current="page"
              >
                <IconViewGrid class="size-2xl mr-4 text-cyan-200" />
                Thống kê
              </NuxtLink>

              <NuxtLink
                :to="{ name: 'admin-game' }"
                class="
                  text-cyan-100
                  hover:text-white hover:bg-cyan-600
                  group
                  flex
                  items-center
                  px-2
                  py-2
                  text-sm
                  leading-6
                  font-medium
                  rounded-md
                "
                aria-current="page"
              >
                <IconGamepad class="size-2xl mr-4 text-cyan-200" />
                Game
              </NuxtLink>

              <NuxtLink
                :to="{ name: 'admin-account' }"
                class="
                  text-cyan-100
                  hover:text-white hover:bg-cyan-600
                  group
                  flex
                  items-center
                  px-2
                  py-2
                  text-sm
                  leading-6
                  font-medium
                  rounded-md
                "
                aria-current="page"
              >
                <IconUserAlien class="size-2xl mr-4 text-cyan-200" />
                Account
              </NuxtLink>
              <NuxtLink
                :to="{ name: 'admin-recharge-phonecard' }"
                class="
                  text-cyan-100
                  hover:text-white hover:bg-cyan-600
                  group
                  flex
                  items-center
                  px-2
                  py-2
                  text-sm
                  leading-6
                  font-medium
                  rounded-md
                "
                aria-current="page"
              >
                <IconCreditCard class="size-2xl mr-4 text-cyan-200" />
                Recharge phonecard
              </NuxtLink>

              <NuxtLink
                :to="{ name: 'admin-coupon' }"
                class="
                  text-cyan-100
                  hover:text-white hover:bg-cyan-600
                  group
                  flex
                  items-center
                  px-2
                  py-2
                  text-sm
                  leading-6
                  font-medium
                  rounded-md
                "
                aria-current="page"
              >
                <IconTicket class="size-2xl mr-4 text-cyan-200" />
                Coupon
              </NuxtLink>
            </div>
            <div class="mt-6 pt-6">
              <div class="px-2 space-y-1">
                <NuxtLink
                  :to="{ name: 'admin-config' }"
                  class="
                    group
                    flex
                    items-center
                    px-2
                    py-2
                    text-sm
                    leading-6
                    font-medium
                    rounded-md
                    text-cyan-100
                    hover:text-white hover:bg-cyan-600
                  "
                >
                  <IconCog class="mr-4 h-6 w-6 text-cyan-200" />
                  Cấu hình
                </NuxtLink>

                <a
                  href="#"
                  class="
                    group
                    flex
                    items-center
                    px-2
                    py-2
                    text-sm
                    leading-6
                    font-medium
                    rounded-md
                    text-cyan-100
                    hover:text-white hover:bg-cyan-600
                  "
                >
                  <!-- Heroicon name: outline/question-mark-circle -->
                  <svg
                    class="mr-4 h-6 w-6 text-cyan-200"
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                    aria-hidden="true"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                    />
                  </svg>
                  Help
                </a>

                <a
                  href="#"
                  class="
                    group
                    flex
                    items-center
                    px-2
                    py-2
                    text-sm
                    leading-6
                    font-medium
                    rounded-md
                    text-cyan-100
                    hover:text-white hover:bg-cyan-600
                  "
                >
                  <!-- Heroicon name: outline/shield-check -->
                  <svg
                    class="mr-4 h-6 w-6 text-cyan-200"
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                    aria-hidden="true"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"
                    />
                  </svg>
                  Privacy
                </a>
              </div>
            </div>
          </nav>
        </div>
      </div>
    </div>

    <div class="flex-1 overflow-auto focus:outline-none" tabindex="0">
      <!-- Header -->
      <div
        class="
          relative
          z-10
          flex-shrink-0 flex
          h-16
          bg-white
          border-b border-gray-200
          lg:border-none
        "
      >
        <button
          class="
            px-4
            border-r border-gray-200
            text-gray-400
            focus:outline-none focus:ring-2 focus:ring-inset focus:ring-cyan-500
            lg:hidden
          "
          @click="showMobileNav = true"
        >
          <span class="sr-only">Open sidebar</span>
          <!-- Heroicon name: outline/menu-alt-1 -->
          <svg
            class="h-6 w-6"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            aria-hidden="true"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h8m-8 6h16"
            />
          </svg>
        </button>
        <!-- Search bar -->
        <div
          class="
            flex-1
            px-4
            flex
            justify-between
            sm:px-6
            lg:max-w-6xl lg:mx-auto lg:px-8
          "
        >
          <div class="flex-1 flex">
            <form class="w-full flex md:ml-0" action="#" method="GET">
              <label for="search_field" class="sr-only">Search</label>
              <div
                class="relative w-full text-gray-400 focus-within:text-gray-600"
              >
                <div
                  class="
                    absolute
                    inset-y-0
                    left-0
                    flex
                    items-center
                    pointer-events-none
                  "
                  aria-hidden="true"
                >
                  <!-- Heroicon name: solid/search -->
                  <svg
                    class="h-5 w-5"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                    aria-hidden="true"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
                      clip-rule="evenodd"
                    />
                  </svg>
                </div>
                <input
                  id="search_field"
                  name="search_field"
                  class="
                    block
                    w-full
                    h-full
                    pl-8
                    pr-3
                    py-2
                    border-transparent
                    text-gray-900
                    placeholder-gray-500
                    focus:outline-none focus:ring-0 focus:border-transparent
                    sm:text-sm
                  "
                  placeholder="Search transactions"
                  type="search"
                />
              </div>
            </form>
          </div>
          <div class="ml-4 flex items-center md:ml-6">
            <button
              class="
                bg-white
                p-1
                rounded-full
                text-gray-400
                hover:text-gray-500
                focus:outline-none
                focus:ring-2
                focus:ring-offset-2
                focus:ring-cyan-500
              "
            >
              <span class="sr-only">View notifications</span>
              <!-- Heroicon name: outline/bell -->
              <svg
                class="h-6 w-6"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                aria-hidden="true"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
                />
              </svg>
            </button>

            <!-- Profile dropdown -->
            <div class="ml-3 relative">
              <div>
                <button
                  id="user-menu"
                  type="button"
                  class="
                    max-w-xs
                    bg-white
                    rounded-full
                    flex
                    items-center
                    text-sm
                    focus:outline-none
                    focus:ring-2
                    focus:ring-offset-2
                    focus:ring-cyan-500
                    lg:p-2 lg:rounded-md lg:hover:bg-gray-50
                  "
                  aria-expanded="false"
                  aria-haspopup="true"
                  @click="showDropMenu = !showDropMenu"
                >
                  <img
                    class="h-8 w-8 rounded-full"
                    src="https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixqx=NiNLTWFfPJ&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
                    alt=""
                  />
                  <span
                    class="
                      hidden
                      ml-3
                      text-gray-700 text-sm
                      font-medium
                      lg:block
                    "
                  >
                    <span class="sr-only">Open user menu for </span>
                    {{ $store.state.auth.profile.name }}
                  </span>
                  <!-- Heroicon name: solid/chevron-down -->
                  <svg
                    class="
                      hidden
                      flex-shrink-0
                      ml-1
                      h-5
                      w-5
                      text-gray-400
                      lg:block
                    "
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                    aria-hidden="true"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                      clip-rule="evenodd"
                    />
                  </svg>
                </button>
              </div>

              <!--
              Dropdown menu, show/hide based on menu state.

              Entering: "transition ease-out duration-100"
                From: "transform opacity-0 scale-95"
                To: "transform opacity-100 scale-100"
              Leaving: "transition ease-in duration-75"
                From: "transform opacity-100 scale-100"
                To: "transform opacity-0 scale-95"
            -->
              <div
                v-show="showDropMenu"
                class="
                  origin-top-right
                  absolute
                  right-0
                  mt-2
                  w-48
                  rounded-md
                  shadow-lg
                  py-1
                  bg-white
                  ring-1 ring-black ring-opacity-5
                  focus:outline-none
                "
                role="menu"
                aria-orientation="vertical"
                aria-labelledby="user-menu"
              >
                <!-- <a
                  href="#"
                  class="
                    block
                    px-4
                    py-2
                    text-sm text-gray-700
                    hover:bg-gray-100
                  "
                  role="menuitem"
                  >Your Profile</a
                >
                <a
                  href="#"
                  class="
                    block
                    px-4
                    py-2
                    text-sm text-gray-700
                    hover:bg-gray-100
                  "
                  role="menuitem"
                  >Settings</a
                > -->
                <a
                  class="
                    block
                    px-4
                    py-2
                    text-sm text-gray-700
                    hover:bg-gray-100
                    cursor-pointer
                  "
                  role="menuitem"
                  @click.prevent="logout"
                >
                  Logout
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
      <main class="flex-1 relative pb-8 overflow-y-auto min-h-screen">
        <Nuxt keep-alive />
      </main>
    </div>
  </div>
</template>

<script>
export default {
  middleware: 'auth',
  data() {
    return {
      showDropMenu: false,
      showMobileNav: false,
    };
  },
  methods: {
    logout() {
      this.$auth.logout().then(() => {
        this.$router.push({ name: 'login' });
      });
    },
  },
};
</script>

<style scoped>
.nuxt-link-exact-active {
  @apply bg-cyan-800 text-white;
}
</style>
