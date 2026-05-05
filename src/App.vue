<template>
  <div class="min-vh-100" style="background: var(--bs-body-bg);">
    <AppNavbar />

    <main class="ems-page-wrapper py-4">
      <!-- Alert -->
      <Transition name="fade">
        <div v-if="alertMsg"
             :class="['alert d-flex align-items-center gap-2 mb-4', alertType === 'ok' ? 'alert-success' : 'alert-danger']"
             role="alert">
          <CircleCheck v-if="alertType === 'ok'" :size="16" />
          <CircleX v-else :size="16" />
          {{ alertMsg }}
        </div>
      </Transition>

      <!-- Stats -->
      <StatCards :employees="employees" />

      <!-- Form -->
      <EmployeeForm
        :form="form"
        :edit-mode="editMode"
        :loading="loading"
        @submit="submitForm"
        @cancel="cancelEdit"
      />

      <!-- Table -->
      <EmployeeTable
        :employees="employees"
        :loading="loading"
        @edit="startEdit"
        @delete="deleteEmp"
        @refresh="fetchEmployees"
      />
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import { CircleCheck, CircleX } from 'lucide-vue-next'

import AppNavbar from './components/AppNavbar.vue'
import StatCards from './components/StatCards.vue'
import EmployeeForm from './components/EmployeeForm.vue'
import EmployeeTable from './components/EmployeeTable.vue'

const API = 'https://69f975c1c509a40d3aa27c47.mockapi.io/employees'

const employees = ref([])
const loading = ref(false)
const editMode = ref(false)
const editId = ref(null)
const alertMsg = ref('')
const alertType = ref('ok')
const form = ref({ EmployeeId: '', name: '', designation: '', department: '', salary: '' })

const flash = (msg, type = 'ok') => {
  alertMsg.value = msg
  alertType.value = type
  setTimeout(() => (alertMsg.value = ''), 3500)
}

const fetchEmployees = async () => {
  loading.value = true
  try {
    const res = await axios.get(API)
    employees.value = res.data
    flash(`${res.data.length} records loaded`, 'ok')
  } catch (e) {
    flash('Fetch failed: ' + (e.response?.status || e.message), 'err')
  } finally {
    loading.value = false
  }
}

const submitForm = async (formData) => {
  const { EmployeeId, name, designation, department, salary } = formData
  if (!EmployeeId || !name || !designation || !department || !salary) {
    flash('Please fill in all fields', 'err')
    return
  }
  loading.value = true
  try {
    if (editMode.value) {
      await axios.put(`${API}/${editId.value}`, formData)
      const i = employees.value.findIndex(e => e.id === editId.value)
      if (i !== -1) employees.value[i] = { ...employees.value[i], ...formData }
      flash('Employee updated successfully', 'ok')
    } else {
      const res = await axios.post(API, formData)
      employees.value.push(res.data)
      flash('Employee added successfully', 'ok')
    }
    resetForm()
  } catch (e) {
    flash('Operation failed: ' + (e.response?.status || e.message), 'err')
  } finally {
    loading.value = false
  }
}

const deleteEmp = async (id) => {
  if (!confirm('Delete this employee record?')) return
  try {
    await axios.delete(`${API}/${id}`)
    employees.value = employees.value.filter(e => e.id !== id)
    flash('Employee deleted', 'ok')
  } catch (e) {
    flash('Delete failed: ' + (e.response?.status || e.message), 'err')
  }
}

const startEdit = (emp) => {
  form.value = {
    EmployeeId: emp.EmployeeId || emp.employeeId || '',
    name: emp.name || '',
    designation: emp.designation || '',
    department: emp.department || '',
    salary: emp.salary || ''
  }
  editMode.value = true
  editId.value = emp.id
}

const cancelEdit = () => resetForm()

const resetForm = () => {
  form.value = { EmployeeId: '', name: '', designation: '', department: '', salary: '' }
  editMode.value = false
  editId.value = null
}

onMounted(fetchEmployees)
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
