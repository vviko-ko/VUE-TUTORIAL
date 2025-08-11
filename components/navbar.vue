<template>
  <header
    class="navbar bg-backgroundDark dark:bg-backgroundDark dark:border-b dark:border-primary/10 sticky top-0 z-10 shadow-sm px-4"
  >
    <!-- Left: Mobile menu toggle -->
    <!-- <nav class="flex-none lg:hidden">
      <label @click="$emit('toggle-drawer')" class="btn btn-square btn-ghost">
        <icon icon="line-md:close-to-menu-alt-transition" class="inline-block w-6 h-6"></icon>
      </label>
    </nav> -->

    <!-- Right section for desktop -->
    <div class="flex-1 flex justify-end items-center gap-3">
      <!-- Search -->
      <div class="form-control hidden md:block">
        <input
          type="text"
          placeholder="Search"
          class="input input-bordered input-primary w-48
                 dark:bg-white/5 dark:backdrop-blur-md
                 dark:[--webkit-backdrop-filter:blur{10px}] dark:border-white/10"
        />
      </div>

      <!-- Notifications -->
      <button class="btn btn-square btn-ghost relative">
        <icon icon="mdi:bell-outline" class="w-6 h-6"></icon>
        <span
          class="absolute top-1 right-1 bg-red-500 text-white text-xs rounded-full px-1"
        >
          3
        </span>
      </button>

      <!-- Profile Dropdown -->
      <div class="dropdown dropdown-end" ref="profileDropdown">
        <label tabindex="0" class="btn btn-ghost btn-circle avatar">
          <div class="w-10 rounded-full">
            <img src="https://via.placeholder.com/150" alt="Profile" />
          </div>
        </label>
        <ul
          tabindex="0"
          class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow bg-base-100 rounded-box w-52 dark:bg-backgroundDark"
        >
          <li>
            <a>
              <icon icon="mdi:account-outline" class="w-5 h-5" />
              Profile
            </a>
          </li>
          <li>
            <a>
              <icon icon="mdi:cog-outline" class="w-5 h-5" />
              Settings
            </a>
          </li>
          <li>
            <a class="text-red-500">
              <icon icon="mdi:logout" class="w-5 h-5" />
              Logout
            </a>
          </li>
        </ul>
      </div>
    </div>
  </header>
</template>

<script setup>
defineEmits(['toggle-drawer'])
</script>
