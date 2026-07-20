<template>
  <div class="app">
    <button class="sidebar-toggle" @click="sidebarOpen = !sidebarOpen" aria-label="Toggle navigation">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm0 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm0 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z" clip-rule="evenodd" />
      </svg>
    </button>

    <aside class="sidebar" :class="{ open: sidebarOpen, collapsed: isCollapsed }">
      <div class="logo">
        <template v-if="!isCollapsed">
          <h1>{{ t('nav.companyName') }}</h1>
          <span class="subtitle">{{ t('nav.subtitle') }}</span>
        </template>
        <div v-else class="logo-mark" :title="t('nav.companyName')">{{ logoInitials }}</div>
      </div>

      <button
        v-if="!isNarrowScreen"
        class="collapse-toggle"
        @click="toggleCollapse"
        :aria-label="isCollapsed ? 'Expand sidebar' : 'Collapse sidebar'"
        :title="isCollapsed ? 'Expand sidebar' : 'Collapse sidebar'"
      >
        <svg viewBox="0 0 20 20" fill="none" :class="{ flipped: isCollapsed }">
          <path d="M12.5 4L7 10L12.5 16" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </button>

      <nav class="nav-tabs">
        <router-link to="/" :class="{ active: $route.path === '/' }" :title="isCollapsed ? t('nav.overview') : null">
          <span class="nav-icon">
            <svg viewBox="0 0 20 20" fill="none"><rect x="2.5" y="2.5" width="6.5" height="6.5" rx="1.2" stroke="currentColor" stroke-width="1.6"/><rect x="11" y="2.5" width="6.5" height="6.5" rx="1.2" stroke="currentColor" stroke-width="1.6"/><rect x="2.5" y="11" width="6.5" height="6.5" rx="1.2" stroke="currentColor" stroke-width="1.6"/><rect x="11" y="11" width="6.5" height="6.5" rx="1.2" stroke="currentColor" stroke-width="1.6"/></svg>
          </span>
          <span class="nav-label">{{ t('nav.overview') }}</span>
        </router-link>
        <router-link to="/inventory" :class="{ active: $route.path === '/inventory' }" :title="isCollapsed ? t('nav.inventory') : null">
          <span class="nav-icon">
            <svg viewBox="0 0 20 20" fill="none"><path d="M10 2.5L17 6.25V13.75L10 17.5L3 13.75V6.25L10 2.5Z" stroke="currentColor" stroke-width="1.6" stroke-linejoin="round"/><path d="M3 6.25L10 10L17 6.25M10 10V17.5" stroke="currentColor" stroke-width="1.6" stroke-linejoin="round"/></svg>
          </span>
          <span class="nav-label">{{ t('nav.inventory') }}</span>
        </router-link>
        <router-link to="/orders" :class="{ active: $route.path === '/orders' }" :title="isCollapsed ? t('nav.orders') : null">
          <span class="nav-icon">
            <svg viewBox="0 0 20 20" fill="none"><path d="M2.5 4.5H4.2L5.7 13.4C5.8 13.9 6.25 14.3 6.75 14.3H14.7C15.2 14.3 15.65 13.95 15.75 13.45L17 6.75H4.7" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/><circle cx="7.5" cy="17" r="1.1" fill="currentColor"/><circle cx="14" cy="17" r="1.1" fill="currentColor"/></svg>
          </span>
          <span class="nav-label">{{ t('nav.orders') }}</span>
        </router-link>
        <router-link to="/spending" :class="{ active: $route.path === '/spending' }" :title="isCollapsed ? t('nav.finance') : null">
          <span class="nav-icon">
            <svg viewBox="0 0 20 20" fill="none"><path d="M10 2.5V17.5" stroke="currentColor" stroke-width="1.6" stroke-linecap="round"/><path d="M13.5 5.5H8.75C7.5 5.5 6.5 6.4 6.5 7.5C6.5 8.6 7.5 9.5 8.75 9.5H11.25C12.5 9.5 13.5 10.4 13.5 11.5C13.5 12.6 12.5 13.5 11.25 13.5H6.5" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/></svg>
          </span>
          <span class="nav-label">{{ t('nav.finance') }}</span>
        </router-link>
        <router-link to="/demand" :class="{ active: $route.path === '/demand' }" :title="isCollapsed ? t('nav.demandForecast') : null">
          <span class="nav-icon">
            <svg viewBox="0 0 20 20" fill="none"><path d="M2.5 15.5L7.5 9.5L11 12L17.5 4.5" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/><path d="M13 4.5H17.5V9" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/></svg>
          </span>
          <span class="nav-label">{{ t('nav.demandForecast') }}</span>
        </router-link>
        <router-link to="/reports" :class="{ active: $route.path === '/reports' }" :title="isCollapsed ? 'Reports' : null">
          <span class="nav-icon">
            <svg viewBox="0 0 20 20" fill="none"><path d="M5.5 2.5H11.5L14.5 5.5V17.5H5.5V2.5Z" stroke="currentColor" stroke-width="1.6" stroke-linejoin="round"/><path d="M7.5 9H12.5M7.5 12H12.5M7.5 15H10.5" stroke="currentColor" stroke-width="1.6" stroke-linecap="round"/></svg>
          </span>
          <span class="nav-label">Reports</span>
        </router-link>
      </nav>
      <div class="sidebar-spacer"></div>
      <div class="sidebar-footer">
        <LanguageSwitcher />
        <ProfileMenu
          @show-profile-details="showProfileDetails = true"
          @show-tasks="showTasks = true"
        />
      </div>
    </aside>

    <div class="sidebar-backdrop" v-if="sidebarOpen" @click="sidebarOpen = false"></div>

    <div class="content">
      <FilterBar />
      <main class="main-content">
        <router-view />
      </main>
    </div>

    <ProfileDetailsModal
      :is-open="showProfileDetails"
      @close="showProfileDetails = false"
    />

    <TasksModal
      :is-open="showTasks"
      :tasks="tasks"
      @close="showTasks = false"
      @add-task="addTask"
      @delete-task="deleteTask"
      @toggle-task="toggleTask"
    />
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted, computed } from 'vue'
import { api } from './api'
import { useAuth } from './composables/useAuth'
import { useI18n } from './composables/useI18n'
import FilterBar from './components/FilterBar.vue'
import ProfileMenu from './components/ProfileMenu.vue'
import ProfileDetailsModal from './components/ProfileDetailsModal.vue'
import TasksModal from './components/TasksModal.vue'
import LanguageSwitcher from './components/LanguageSwitcher.vue'

export default {
  name: 'App',
  components: {
    FilterBar,
    ProfileMenu,
    ProfileDetailsModal,
    TasksModal,
    LanguageSwitcher
  },
  setup() {
    const { currentUser } = useAuth()
    const { t } = useI18n()
    const showProfileDetails = ref(false)
    const showTasks = ref(false)
    const sidebarOpen = ref(false)
    const apiTasks = ref([])

    // Sidebar collapse (icons-only rail) state, persisted across reloads
    const NARROW_BREAKPOINT = 1024
    const collapsed = ref(localStorage.getItem('sidebarCollapsed') === 'true')
    const isNarrowScreen = ref(typeof window !== 'undefined' && window.innerWidth < NARROW_BREAKPOINT)

    // Below the breakpoint the rail is always icons-only regardless of the manual preference
    const isCollapsed = computed(() => isNarrowScreen.value || collapsed.value)

    const logoInitials = computed(() => {
      const name = t('nav.companyName') || ''
      return name
        .split(/\s+/)
        .filter(Boolean)
        .slice(0, 2)
        .map(word => word[0])
        .join('')
        .toUpperCase()
    })

    const toggleCollapse = () => {
      collapsed.value = !collapsed.value
      localStorage.setItem('sidebarCollapsed', String(collapsed.value))
    }

    const handleResize = () => {
      isNarrowScreen.value = window.innerWidth < NARROW_BREAKPOINT
    }

    // Merge mock tasks from currentUser with API tasks
    const tasks = computed(() => {
      return [...currentUser.value.tasks, ...apiTasks.value]
    })

    const loadTasks = async () => {
      try {
        apiTasks.value = await api.getTasks()
      } catch (err) {
        console.error('Failed to load tasks:', err)
      }
    }

    const addTask = async (taskData) => {
      try {
        const newTask = await api.createTask(taskData)
        // Add new task to the beginning of the array
        apiTasks.value.unshift(newTask)
      } catch (err) {
        console.error('Failed to add task:', err)
      }
    }

    const deleteTask = async (taskId) => {
      try {
        // Check if it's a mock task (from currentUser)
        const isMockTask = currentUser.value.tasks.some(t => t.id === taskId)

        if (isMockTask) {
          // Remove from mock tasks
          const index = currentUser.value.tasks.findIndex(t => t.id === taskId)
          if (index !== -1) {
            currentUser.value.tasks.splice(index, 1)
          }
        } else {
          // Remove from API tasks
          await api.deleteTask(taskId)
          apiTasks.value = apiTasks.value.filter(t => t.id !== taskId)
        }
      } catch (err) {
        console.error('Failed to delete task:', err)
      }
    }

    const toggleTask = async (taskId) => {
      try {
        // Check if it's a mock task (from currentUser)
        const mockTask = currentUser.value.tasks.find(t => t.id === taskId)

        if (mockTask) {
          // Toggle mock task status
          mockTask.status = mockTask.status === 'pending' ? 'completed' : 'pending'
        } else {
          // Toggle API task
          const updatedTask = await api.toggleTask(taskId)
          const index = apiTasks.value.findIndex(t => t.id === taskId)
          if (index !== -1) {
            apiTasks.value[index] = updatedTask
          }
        }
      } catch (err) {
        console.error('Failed to toggle task:', err)
      }
    }

    onMounted(() => {
      loadTasks()
      window.addEventListener('resize', handleResize)
    })

    onUnmounted(() => {
      window.removeEventListener('resize', handleResize)
    })

    return {
      t,
      showProfileDetails,
      showTasks,
      sidebarOpen,
      isCollapsed,
      isNarrowScreen,
      toggleCollapse,
      logoInitials,
      tasks,
      addTask,
      deleteTask,
      toggleTask
    }
  }
}
</script>

<style>
:root {
  /* Surfaces */
  --color-app-bg: #f8fafc;
  --color-surface: #ffffff;
  --color-surface-muted: #f1f5f9;

  /* Borders */
  --color-border: #e2e8f0;
  --color-border-strong: #cbd5e1;

  /* Text */
  --color-text: #0f172a;
  --color-text-secondary: #475569;
  --color-text-muted: #64748b;
  --color-text-inverse: #f8fafc;

  /* Brand / accent */
  --color-brand: #2563eb;
  --color-brand-hover: #1d4ed8;
  --color-brand-soft: #eff6ff;
  --color-focus-ring: #3b82f6;

  /* Semantic */
  --color-success: #059669;
  --color-info: #2563eb;
  --color-warning: #ea580c;
  --color-danger: #dc2626;

  /* Sidebar (dark slate) */
  --sidebar-width: 248px;
  --sidebar-width-collapsed: 68px;
  --sidebar-bg: #0f172a;
  --sidebar-text: #cbd5e1;
  --sidebar-text-active: #ffffff;
  --sidebar-item-active-bg: rgba(37, 99, 235, 0.18);
  --sidebar-item-hover-bg: rgba(148, 163, 184, 0.12);

  /* Spacing scale */
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-5: 1.25rem;
  --space-6: 1.5rem;
  --space-8: 2rem;

  /* Radii */
  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 14px;

  /* Shadows */
  --shadow-sm: 0 1px 2px rgba(15, 23, 42, 0.06);
  --shadow-md: 0 4px 12px rgba(15, 23, 42, 0.08);

  /* Typography */
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;

  /* Layout */
  --content-max-width: 1600px;
  --topbar-height: 64px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: var(--font-sans);
  background: var(--color-app-bg);
  color: #1e293b;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.app {
  display: flex;
  min-height: 100vh;
}

.sidebar-toggle {
  display: none;
  position: fixed;
  top: var(--space-3);
  left: var(--space-3);
  z-index: 200;
  width: 40px;
  height: 40px;
  align-items: center;
  justify-content: center;
  background: var(--sidebar-bg);
  color: var(--color-text-inverse);
  border: none;
  border-radius: var(--radius-sm);
  cursor: pointer;
}

.sidebar-toggle svg {
  width: 20px;
  height: 20px;
}

.sidebar {
  flex-shrink: 0;
  width: var(--sidebar-width);
  background: var(--sidebar-bg);
  display: flex;
  flex-direction: column;
  padding: var(--space-5) var(--space-3);
  position: sticky;
  top: 0;
  height: 100vh;
  overflow-y: auto;
  transition: width 0.2s ease;
}

.sidebar.collapsed {
  width: var(--sidebar-width-collapsed);
  padding-left: var(--space-2);
  padding-right: var(--space-2);
  overflow-x: hidden;
}

.sidebar-backdrop {
  display: none;
}

.logo {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
  padding: var(--space-2) var(--space-3) var(--space-5);
}

.logo h1 {
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--sidebar-text-active);
  letter-spacing: -0.025em;
}

.subtitle {
  font-size: 0.75rem;
  color: var(--sidebar-text);
  font-weight: 400;
}

.logo-mark {
  width: 36px;
  height: 36px;
  border-radius: var(--radius-sm);
  background: var(--sidebar-item-active-bg);
  color: var(--sidebar-text-active);
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 0.875rem;
  letter-spacing: 0.025em;
  margin: 0 auto;
}

.collapse-toggle {
  display: flex;
  align-items: center;
  justify-content: center;
  align-self: flex-end;
  width: 28px;
  height: 28px;
  margin: 0 var(--space-3) var(--space-3);
  background: var(--sidebar-item-hover-bg);
  color: var(--sidebar-text);
  border: none;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all 0.2s ease;
}

.collapse-toggle:hover {
  color: var(--sidebar-text-active);
  background: var(--sidebar-item-active-bg);
}

.collapse-toggle svg {
  width: 16px;
  height: 16px;
  transition: transform 0.2s ease;
}

.collapse-toggle svg.flipped {
  transform: rotate(180deg);
}

.sidebar.collapsed .collapse-toggle {
  align-self: center;
  margin: 0 0 var(--space-3);
}

.nav-tabs {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
}

.nav-tabs a {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  padding: var(--space-3) var(--space-4);
  color: var(--sidebar-text);
  text-decoration: none;
  font-weight: 500;
  font-size: 0.938rem;
  border-radius: var(--radius-sm);
  transition: all 0.2s ease;
  position: relative;
}

.nav-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  width: 20px;
  height: 20px;
}

.nav-icon svg {
  width: 20px;
  height: 20px;
}

.nav-label {
  white-space: nowrap;
  overflow: hidden;
}

.sidebar.collapsed .nav-tabs a {
  justify-content: center;
  padding: var(--space-3);
}

.sidebar.collapsed .nav-label,
.sidebar.collapsed .language-label,
.sidebar.collapsed .profile-name,
.sidebar.collapsed .chevron {
  display: none;
}

.sidebar.collapsed .sidebar-footer {
  align-items: center;
}

.sidebar.collapsed .sidebar-footer .language-button,
.sidebar.collapsed .sidebar-footer .profile-button {
  padding: var(--space-2);
  justify-content: center;
}

.nav-tabs a:hover {
  color: var(--sidebar-text-active);
  background: var(--sidebar-item-hover-bg);
}

.nav-tabs a.active {
  color: var(--sidebar-text-active);
  background: var(--sidebar-item-active-bg);
}

.nav-tabs a.active::before {
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  width: 3px;
  border-radius: var(--radius-sm) 0 0 var(--radius-sm);
  background: var(--color-brand);
}

.sidebar-spacer {
  flex: 1;
}

.sidebar-footer {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
  padding-top: var(--space-4);
  border-top: 1px solid rgba(148, 163, 184, 0.2);
}

.content {
  flex: 1;
  min-width: 0;
  display: flex;
  flex-direction: column;
}

.main-content {
  flex: 1;
  width: 100%;
  padding: var(--space-6) var(--space-8);
}

.main-content > * {
  max-width: var(--content-max-width);
  margin-left: auto;
  margin-right: auto;
}

.page-header {
  margin-bottom: var(--space-6);
}

.page-header h2 {
  font-size: 1.875rem;
  font-weight: 700;
  color: var(--color-text);
  margin-bottom: var(--space-1);
  letter-spacing: -0.025em;
}

.page-header p {
  color: var(--color-text-muted);
  font-size: 0.938rem;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: var(--space-4);
  margin-bottom: var(--space-6);
}

.stat-card {
  background: var(--color-surface);
  padding: var(--space-5);
  border-radius: var(--radius-md);
  border: 1px solid var(--color-border);
  box-shadow: var(--shadow-sm);
  transition: all 0.2s ease;
}

.stat-card:hover {
  border-color: var(--color-border-strong);
  box-shadow: var(--shadow-md);
}

.stat-label {
  color: var(--color-text-muted);
  font-size: 0.875rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: var(--space-3);
}

.stat-value {
  font-size: 2.25rem;
  font-weight: 700;
  color: var(--color-text);
  letter-spacing: -0.025em;
}

.stat-card.warning .stat-value {
  color: var(--color-warning);
}

.stat-card.success .stat-value {
  color: var(--color-success);
}

.stat-card.danger .stat-value {
  color: var(--color-danger);
}

.stat-card.info .stat-value {
  color: var(--color-info);
}

.card {
  background: var(--color-surface);
  border-radius: var(--radius-md);
  padding: var(--space-5);
  border: 1px solid var(--color-border);
  box-shadow: var(--shadow-sm);
  margin-bottom: var(--space-5);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--space-4);
  padding-bottom: var(--space-3);
  border-bottom: 1px solid var(--color-border);
}

.card-title {
  font-size: 1.125rem;
  font-weight: 700;
  color: var(--color-text);
  letter-spacing: -0.025em;
}

.table-container {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

thead {
  background: var(--color-app-bg);
  border-top: 1px solid var(--color-border);
  border-bottom: 1px solid var(--color-border);
}

th {
  text-align: left;
  padding: var(--space-2) var(--space-3);
  font-weight: 600;
  color: var(--color-text-secondary);
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

td {
  padding: var(--space-2) var(--space-3);
  border-top: 1px solid var(--color-surface-muted);
  color: #334155;
  font-size: 0.875rem;
}

tbody tr {
  transition: background-color 0.15s ease;
}

tbody tr:hover {
  background: var(--color-app-bg);
}

.badge {
  display: inline-block;
  padding: 0.313rem var(--space-3);
  border-radius: var(--radius-sm);
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.025em;
}

.badge.success {
  background: #d1fae5;
  color: #065f46;
}

.badge.warning {
  background: #fed7aa;
  color: #92400e;
}

.badge.danger {
  background: #fecaca;
  color: #991b1b;
}

.badge.info {
  background: #dbeafe;
  color: #1e40af;
}

.badge.increasing {
  background: #d1fae5;
  color: #065f46;
}

.badge.decreasing {
  background: #fecaca;
  color: #991b1b;
}

.badge.stable {
  background: #e0e7ff;
  color: #3730a3;
}

.badge.high {
  background: #fecaca;
  color: #991b1b;
}

.badge.medium {
  background: #fed7aa;
  color: #92400e;
}

.badge.low {
  background: #dbeafe;
  color: #1e40af;
}

.loading {
  text-align: center;
  padding: var(--space-8) 0;
  color: var(--color-text-muted);
  font-size: 0.938rem;
}

.error {
  background: #fef2f2;
  border: 1px solid #fecaca;
  color: #991b1b;
  padding: var(--space-4);
  border-radius: var(--radius-md);
  margin: var(--space-4) 0;
  font-size: 0.938rem;
}

@media (max-width: 1024px) {
  /* Below this breakpoint the sidebar auto-collapses to an icons-only rail
     (see isNarrowScreen in App.vue) instead of the off-canvas hamburger menu. */
  .sidebar-toggle {
    display: none;
  }

  .sidebar-backdrop {
    display: none;
  }

  .main-content {
    padding: var(--space-6) var(--space-4);
  }
}
</style>
