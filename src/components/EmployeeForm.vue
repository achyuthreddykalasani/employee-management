<template>
  <div class="card mb-4">
    <div class="card-body p-4">
      <div class="d-flex align-items-center justify-content-between mb-4">
        <div class="d-flex align-items-center gap-2">
          <div class="ems-icon-box" :style="{
            background: editMode ? '#FEF3C7' : 'var(--bs-primary-bg-subtle)',
            color: editMode ? '#D97706' : 'var(--bs-primary)'
          }">
            <SquarePen v-if="editMode" :size="16" />
            <Plus v-else :size="16" />
          </div>
          <h6 class="mb-0 fw-semibold" style="font-family: var(--ems-heading-font);">
            {{ editMode ? 'Edit Employee Record' : 'Add New Employee' }}
          </h6>
        </div>
        <button v-if="editMode" class="ems-action-btn" @click="$emit('cancel')" title="Cancel editing">
          <X :size="16" />
        </button>
      </div>

      <div class="row g-3">
        <div class="col-md-6 col-lg-4">
          <label class="form-label">Employee ID</label>
          <input class="form-control" v-model="localForm.EmployeeId"
                 placeholder="e.g. EMP001" :readonly="editMode">
        </div>
        <div class="col-md-6 col-lg-4">
          <label class="form-label">Full Name</label>
          <input class="form-control" v-model="localForm.name" placeholder="e.g. Ravi Kumar">
        </div>
        <div class="col-md-6 col-lg-4">
          <label class="form-label">Designation</label>
          <input class="form-control" v-model="localForm.designation" placeholder="e.g. Software Engineer">
        </div>
        <div class="col-md-6 col-lg-4">
          <label class="form-label">Department</label>
          <select class="form-select" v-model="localForm.department">
            <option value="">Select department</option>
            <option v-for="dept in departments" :key="dept">{{ dept }}</option>
          </select>
        </div>
        <div class="col-md-6 col-lg-4">
          <label class="form-label">Salary (₹)</label>
          <input class="form-control" type="number" v-model="localForm.salary" placeholder="e.g. 55000">
        </div>
      </div>

      <div class="d-flex gap-2 mt-4 pt-2 border-top">
        <button class="btn btn-primary d-flex align-items-center gap-2" @click="handleSubmit" :disabled="loading">
          <span v-if="loading" class="spinner-border spinner-border-sm"></span>
          <Check v-else :size="16" />
          {{ loading ? 'Please wait...' : (editMode ? 'Update Employee' : 'Add Employee') }}
        </button>
        <button v-if="editMode" class="btn btn-outline-primary d-flex align-items-center gap-2" @click="$emit('cancel')">
          <X :size="16" />
          Cancel
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, watch } from 'vue'
import { Plus, SquarePen, X, Check } from 'lucide-vue-next'

const departments = ['Engineering', 'HR', 'Finance', 'Marketing', 'Operations']

const props = defineProps({
  form: { type: Object, required: true },
  editMode: { type: Boolean, default: false },
  loading: { type: Boolean, default: false }
})

const emit = defineEmits(['submit', 'cancel'])

const localForm = reactive({ ...props.form })

watch(() => props.form, (newForm) => {
  Object.assign(localForm, newForm)
}, { deep: true })

const handleSubmit = () => {
  emit('submit', { ...localForm })
}
</script>
