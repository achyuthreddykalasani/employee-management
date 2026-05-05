<template>
  <div class="row g-3 mb-4">
    <div class="col-6 col-lg-3" v-for="stat in stats" :key="stat.label">
      <div class="ems-stat-card">
        <div class="d-flex align-items-start gap-3">
          <div class="ems-icon-box" :style="{ background: stat.iconBg, color: stat.iconColor }">
            <component :is="stat.icon" :size="16" />
          </div>
          <div>
            <div class="ems-stat-label mb-1">{{ stat.label }}</div>
            <div class="ems-stat-value" :class="stat.valueClass || 'fs-4'">{{ stat.value }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { Users, Building, Banknote, Wifi } from 'lucide-vue-next'

const props = defineProps({
  employees: { type: Array, required: true }
})

const uniqueDepts = computed(() =>
  new Set(props.employees.map(e => e.department).filter(Boolean)).size
)

const avgSalary = computed(() => {
  if (!props.employees.length) return '₹0'
  const avg = Math.round(
    props.employees.reduce((s, e) => s + Number(e.salary || 0), 0) / props.employees.length
  )
  return '₹' + avg.toLocaleString('en-IN')
})

const stats = computed(() => [
  {
    label: 'Total Employees',
    value: props.employees.length,
    icon: Users,
    iconBg: 'var(--bs-primary-bg-subtle)',
    iconColor: 'var(--bs-primary)',
    valueClass: 'fs-4'
  },
  {
    label: 'Departments',
    value: uniqueDepts.value,
    icon: Building,
    iconBg: '#EDE9FE',
    iconColor: '#7C3AED',
    valueClass: 'fs-4'
  },
  {
    label: 'Avg Salary',
    value: avgSalary.value,
    icon: Banknote,
    iconBg: '#FEF3C7',
    iconColor: '#D97706',
    valueClass: 'fs-5'
  },
  {
    label: 'API Status',
    value: 'Live',
    icon: Wifi,
    iconBg: '#D1FAE5',
    iconColor: '#059669',
    valueClass: 'fs-5'
  }
])
</script>
