<template>
  <nav class="navbar py-3 bg-white">
    <div class="ems-page-wrapper w-100">
      <div class="d-flex justify-content-between align-items-center w-100">
        <div class="d-flex align-items-center gap-3">
          <div class="ems-icon-box" style="background: var(--bs-primary); color: #fff;">
            <Users :size="18" />
          </div>
          <div>
            <h1 class="fs-6 fw-bold mb-0" style="font-family: var(--ems-heading-font);">
              Employee Management
            </h1>
            <span class="text-muted" style="font-size: 0.75rem;">Dashboard Overview</span>
          </div>
        </div>
        <div class="d-flex align-items-center gap-2">
          <span class="badge rounded-pill d-flex align-items-center gap-1"
                style="background: var(--bs-primary-bg-subtle); color: var(--bs-primary); padding: 0.4rem 0.75rem; font-size: 0.75rem;">
            <span style="width: 6px; height: 6px; border-radius: 50%; background: var(--bs-success); display: inline-block;"></span>
            API Connected
          </span>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { Users } from 'lucide-vue-next'
</script>
