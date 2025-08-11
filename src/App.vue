<template>
  <div class="flex h-screen bg-gray-900 text-gray-200">
    <!-- Sidebar -->
    <aside
      :class="[
        'bg-gray-800 shadow-md flex flex-col transition-all duration-300',
        sidebarOpen ? 'w-64' : 'w-16'
      ]"
    >
      <div class="flex items-center justify-between p-4 border-b border-gray-700">
        <h1 v-if="sidebarOpen" class="text-lg font-bold">Admin</h1>
        <button @click="toggleSidebar" class="p-2 rounded hover:bg-gray-700">
          <icon icon="mdi:menu" class="w-6 h-6" />
        </button>
      </div>

      <nav class="flex-1 p-2 space-y-2">
        <a href="#" class="flex items-center p-2 rounded hover:bg-gray-700">
          <icon icon="mdi:view-dashboard-outline" class="w-5 h-5" />
          <span v-if="sidebarOpen" class="ml-3">Dashboard</span>
        </a>

        <details :open="sidebarOpen" class="group">
          <summary class="flex items-center p-2 rounded hover:bg-gray-700 cursor-pointer">
            <icon icon="mdi:account-outline" class="w-5 h-5" />
            <span v-if="sidebarOpen" class="ml-3">Users</span>
          </summary>
          <div class="pl-8">
            <a href="#" class="block p-2 text-sm rounded hover:bg-gray-700">All Users</a>
            <a href="#" class="block p-2 text-sm rounded hover:bg-gray-700">Add User</a>
          </div>
        </details>

        <a href="#" class="flex items-center p-2 rounded hover:bg-gray-700">
          <icon icon="mdi:cog-outline" class="w-5 h-5" />
          <span v-if="sidebarOpen" class="ml-3">Settings</span>
        </a>
      </nav>
    </aside>

    <!-- Main Content -->
    <div class="flex-1 flex flex-col">
      <!-- Navbar -->
      <header class="bg-gray-800 px-4 py-2 flex justify-between items-center border-b border-gray-700">
        <div></div>
        <div class="flex items-center space-x-4">
          <!-- Search -->
          <input
            type="text"
            placeholder="Search..."
            class="hidden md:block px-3 py-1 border border-gray-600 rounded-lg focus:outline-none bg-gray-700 text-gray-200"
          />

          <!-- Notification -->
          <button class="relative p-2 rounded hover:bg-gray-700">
            <icon icon="mdi:bell-outline" class="w-6 h-6" />
            <span class="absolute top-0 right-0 w-2 h-2 bg-red-500 rounded-full"></span>
          </button>

          <!-- Profile Dropdown -->
          <div class="relative" @click.away="dropdownOpen = false">
            <button @click="dropdownOpen = !dropdownOpen" class="flex items-center space-x-2">
              <img src="https://via.placeholder.com/40" class="w-8 h-8 rounded-full" alt="Profile" />
              <span class="hidden md:inline font-medium">John Doe</span>
              <icon icon="mdi:chevron-down" class="w-4 h-4" />
            </button>

            <div
              v-if="dropdownOpen"
              class="absolute right-0 mt-2 w-56 bg-gray-800 shadow-lg rounded-lg z-50 border border-gray-700"
            >
              <div class="p-2 border-b border-gray-700">
                <p class="text-sm font-semibold">John Doe</p>
                <p class="text-xs text-gray-400">Admin</p>
              </div>
              <ul class="p-2">
                <li class="menu-title">Account</li>
                <li><a href="#" class="block p-2 hover:bg-gray-700">Profile</a></li>
                <li><a href="#" class="block p-2 hover:bg-gray-700">Messages</a></li>

                <li class="menu-title mt-2">Settings</li>
                <li>
                  <details>
                    <summary class="p-2 cursor-pointer hover:bg-gray-700">Preferences</summary>
                    <ul class="pl-6">
                      <li><a href="#" class="block p-2 hover:bg-gray-700">Theme</a></li>
                      <li><a href="#" class="block p-2 hover:bg-gray-700">Privacy</a></li>
                    </ul>
                  </details>
                </li>
              </ul>
              <div class="border-t border-gray-700 p-2">
                <a href="#" class="block p-2 text-red-500 hover:bg-gray-700">Logout</a>
              </div>
            </div>
          </div>
        </div>
      </header>

      <!-- Dashboard Content -->
      <main class="flex-1 p-4 overflow-y-auto">
        <h2 class="text-xl font-bold mb-4">Dashboard Overview</h2>

        <!-- Charts -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 mb-6">
          <div class="bg-gray-800 p-4 shadow rounded-lg">
            <h3 class="mb-2 font-semibold">Sales Overview</h3>
            <LineChart />
          </div>
          <div class="bg-gray-800 p-4 shadow rounded-lg">
            <h3 class="mb-2 font-semibold">Users Growth</h3>
            <BarChart />
          </div>
          <div class="bg-gray-800 p-4 shadow rounded-lg">
            <h3 class="mb-2 font-semibold">Revenue Sources</h3>
            <DoughnutChart />
          </div>
          <div class="bg-gray-800 p-4 shadow rounded-lg">
            <h3 class="mb-2 font-semibold">Performance Radar</h3>
            <RadarChart />
          </div>
        </div>

        <!-- Table -->
        <div class="bg-gray-800 p-4 shadow rounded-lg">
          <h3 class="mb-2 font-semibold">Recent Activity</h3>
          <table class="w-full text-left border-collapse">
            <thead>
              <tr class="border-b border-gray-700">
                <th class="p-2">User</th>
                <th class="p-2">Action</th>
                <th class="p-2">Date</th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="(item, index) in tableData"
                :key="index"
                class="border-b border-gray-700 hover:bg-gray-700"
              >
                <td class="p-2">{{ item.user }}</td>
                <td class="p-2">{{ item.action }}</td>
                <td class="p-2">{{ item.date }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { Icon } from "@iconify/vue";
import LineChart from "../components/LineChart.vue";
import BarChart from "../components/BarChart.vue";
import DoughnutChart from "../components/DoughnutChart.vue";
import RadarChart from "../components/RadarChart.vue";

const sidebarOpen = ref(true);
const dropdownOpen = ref(false);

const tableData = ref([
  { user: "Alice", action: "Logged in", date: "2025-08-01" },
  { user: "Bob", action: "Updated profile", date: "2025-08-02" },
  { user: "Charlie", action: "Uploaded file", date: "2025-08-03" },
]);

function toggleSidebar() {
  sidebarOpen.value = !sidebarOpen.value;
}
</script>

<style>
.menu-title {
  font-size: 0.75rem;
  text-transform: uppercase;
  color: #9ca3af;
  padding: 0.25rem 0.5rem;
}
</style>
