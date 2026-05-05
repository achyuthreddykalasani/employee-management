<template>
  <div class="card">
    <div class="card-body p-4">
      <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-2">
        <div class="d-flex align-items-center gap-2">
          <div class="ems-icon-box" style="background: var(--bs-primary-bg-subtle); color: var(--bs-primary);">
            <Users :size="16" />
          </div>
          <h6 class="mb-0 fw-semibold" style="font-family: var(--ems-heading-font);">
            Employee Records
          </h6>
          <span class="badge rounded-pill"
                style="background: var(--ems-bg-subtle); color: var(--ems-text-muted); font-size: 0.7rem;">
            {{ filtered.length }} {{ filtered.length === 1 ? 'record' : 'records' }}
          </span>
        </div>
        <div class="d-flex gap-2 align-items-center">
          <div class="position-relative">
            <Search :size="14" class="position-absolute"
                    style="left: 0.75rem; top: 50%; transform: translateY(-50%); color: var(--ems-text-muted);" />
            <input class="form-control form-control-sm" style="width: 220px; padding-left: 2.25rem;"
                   v-model="search" placeholder="Search by name or ID...">
          </div>
          <button class="btn btn-outline-primary btn-sm d-flex align-items-center gap-1" @click="$emit('refresh')">
            <RefreshCw :size="14" />
            <span class="d-none d-md-inline">Refresh</span>
          </button>
        </div>
      </div>

      <!-- Loading state -->
      <div v-if="loading && employees.length === 0" class="text-center py-5">
        <div class="spinner-border text-primary mb-3" role="status" style="width: 2rem; height: 2rem;">
          <span class="visually-hidden">Loading...</span>
        </div>
        <p class="text-muted mb-0" style="font-size: 0.875rem;">Loading employee records...</p>
      </div>

      <!-- Empty state -->
      <div v-else-if="filtered.length === 0" class="text-center py-5">
        <div class="ems-icon-box mx-auto mb-3"
             style="width: 3.5rem; height: 3.5rem; background: var(--ems-bg-subtle); color: var(--ems-text-muted);">
          <Users :size="24" />
        </div>
        <p class="text-muted mb-1 fw-medium" style="font-size: 0.875rem;">No records found</p>
        <p class="text-muted mb-0" style="font-size: 0.8125rem;">Add an employee using the form above.</p>
      </div>

      <!-- Table -->
      <div v-else class="table-responsive">
        <table class="table table-hover align-middle mb-0">
          <thead>
            <tr>
              <th>Emp ID</th>
              <th>Name</th>
              <th>Designation</th>
              <th>Department</th>
              <th>Salary</th>
              <th class="text-end">Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="emp in filtered" :key="emp.id">
              <td>
                <span class="fw-semibold" style="color: var(--bs-primary); font-size: 0.8125rem;">
                  {{ emp.EmployeeId || emp.employeeId }}
                </span>
              </td>
              <td>
                <div class="d-flex align-items-center gap-2">
                  <div class="ems-icon-box"
                       style="width: 2rem; height: 2rem; background: var(--ems-bg-subtle); color: var(--ems-text-muted);">
                    <User :size="14" />
                  </div>
                  <span class="fw-medium" style="font-size: 0.875rem;">{{ emp.name }}</span>
                </div>
              </td>
              <td>
                <span class="text-muted" style="font-size: 0.8125rem;">{{ emp.designation }}</span>
              </td>
              <td>
                <span class="badge rounded-pill" :style="deptStyle(emp.department)">
                  {{ emp.department }}
                </span>
              </td>
              <td>
                <span class="fw-semibold" style="font-size: 0.8125rem; color: var(--bs-heading-color);">
                  ₹{{ Number(emp.salary || 0).toLocaleString('en-IN') }}
                </span>
              </td>
              <td>
                <div class="d-flex gap-1 justify-content-end">
                  <button class="ems-action-btn ems-action-btn-edit" @click="$emit('edit', emp)" title="Edit employee">
                    <Pencil :size="14" />
                  </button>
                  <button class="ems-action-btn ems-action-btn-delete" @click="$emit('delete', emp.id)" title="Delete employee">
                    <Trash2 :size="14" />
                  </button>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { Users, User, Pencil, Trash2, Search, RefreshCw } from 'lucide-vue-next'

const props = defineProps({
  employees: { type: Array, required: true },
  loading: { type: Boolean, default: false }
})

defineEmits(['edit', 'delete', 'refresh'])

const search = ref('')

const filtered = computed(() =>
  props.employees.filter(e => {
    const q = search.value.toLowerCase()
    return (e.name || '').toLowerCase().includes(q) ||
           String(e.EmployeeId || e.employeeId || '').toLowerCase().includes(q)
  })
)

const deptColors = {
  Engineering: { bg: '#D7E7E7', color: '#2F4F4F' },
  HR: { bg: '#EDE9FE', color: '#7C3AED' },
  Finance: { bg: '#FEF3C7', color: '#D97706' },
  Marketing: { bg: '#FCE7F3', color: '#DB2777' },
  Operations: { bg: '#FFEDD5', color: '#EA580C' }
}

const deptStyle = (dept) => {
  const c = deptColors[dept] || { bg: '#F1F5F9', color: '#64748B' }
  return {
    background: c.bg,
    color: c.color,
    fontWeight: '500',
    fontSize: '0.75rem',
    padding: '0.3rem 0.65rem'
  }
}
</script>
