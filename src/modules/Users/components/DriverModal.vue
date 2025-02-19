<template>
  <div
    class="modal fade"
    id="driverModal"
    tabindex="-1"
    aria-hidden="true"
    data-bs-backdrop="false"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">
            {{ mode === "add" ? "Add New Driver" : "Edit Driver" }}
          </h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <form @submit.prevent="handleSubmit">
          <div class="modal-body">
            <!-- Driver Name and Mobile -->
            <div class="row mb-3">
              <div class="col-md-6">
                <label for="name" class="form-label"
                  >Driver Name <span class="text-danger">*</span></label
                >
                <input
                  type="text"
                  id="name"
                  class="form-control"
                  v-model="userData.name"
                  required
                  minlength="3"
                />
              </div>
              <div class="col-md-6">
                <label for="mobile" class="form-label"
                  >Mobile # <span class="text-danger">*</span></label
                >
                <input
                  type="text"
                  id="mobile"
                  class="form-control"
                  v-model="userData.mobile"
                  required
                  pattern="^[0-9]+$"
                />
              </div>
            </div>

            <!-- Email and Position -->
            <div class="row mb-3">
              <div class="col-md-6">
                <label for="email" class="form-label"
                  >Email <span class="text-danger">*</span></label
                >
                <input
                  type="email"
                  id="email"
                  class="form-control"
                  v-model="userData.email"
                  required
                />
              </div>
              <div class="col-md-6">
                <label for="position" class="form-label">Position</label>
                <input
                  type="text"
                  id="position"
                  class="form-control"
                  v-model="userData.position"
                />
              </div>
            </div>

            <!-- License Info -->
            <div class="row mb-3">
              <div class="col-md-6">
                <label for="licenseNumber" class="form-label"
                  >License # <span class="text-danger">*</span></label
                >
                <input
                  type="text"
                  id="licenseNumber"
                  class="form-control"
                  v-model="userData.licenseNumber"
                  required
                />
              </div>
              <div class="col-md-6">
                <label for="licenseType" class="form-label">License Type</label>
                <select
                  id="licenseType"
                  class="form-select"
                  v-model="userData.licenseType"
                >
                  <option value="">Select License Type</option>
                  <option value="Type A">Type A</option>
                  <option value="Type B">Type B</option>
                </select>
              </div>
            </div>

            <!-- License Dates -->
            <div class="row mb-3">
              <div class="col-md-6">
                <label for="licenseIssue" class="form-label"
                  >License Issue Date</label
                >
                <input
                  type="date"
                  id="licenseIssue"
                  class="form-control"
                  v-model="userData.licenseIssue"
                />
              </div>
              <div class="col-md-6">
                <label for="licenseExpiry" class="form-label"
                  >License Expiry Date <span class="text-danger">*</span></label
                >
                <input
                  type="date"
                  id="licenseExpiry"
                  class="form-control"
                  v-model="userData.licenseExpiry"
                  required
                />
              </div>
            </div>

            <!-- Birth Date and Phone -->
            <div class="row mb-3">
              <div class="col-md-6">
                <label for="birthDate" class="form-label">Birth Date</label>
                <input
                  type="date"
                  id="birthDate"
                  class="form-control"
                  v-model="userData.birthDate"
                />
              </div>
              <div class="col-md-6">
                <label for="phone" class="form-label">Phone</label>
                <input
                  type="text"
                  id="phone"
                  class="form-control"
                  v-model="userData.phone"
                />
              </div>
            </div>

            <!-- Addresses -->
            <div class="row mb-3">
              <div class="col-md-6">
                <label for="homeAddress" class="form-label">Home Address</label>
                <input
                  type="text"
                  id="homeAddress"
                  class="form-control"
                  v-model="userData.homeAddress"
                />
              </div>
              <div class="col-md-6">
                <label for="workAddress" class="form-label">Work Address</label>
                <input
                  type="text"
                  id="workAddress"
                  class="form-control"
                  v-model="userData.workAddress"
                />
              </div>
            </div>
          </div>

          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
              @click="resetForm"
            >
              Cancel
            </button>
            <button type="submit" class="btn btn-primary">
              {{ mode === "add" ? "Add Driver" : "Save Changes" }}
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  mode: {
    type: String,
    required: true, // 'add' or 'edit'
  },
  user: {
    type: Object,
    default: () => ({
      name: "",
      mobile: "",
      email: "",
      position: "",
      licenseNumber: "",
      licenseType: "",
      licenseIssue: "",
      licenseExpiry: "",
      birthDate: "",
      phone: "",
      homeAddress: "",
      workAddress: "",
    }),
  },
});

const emit = defineEmits(["submit"]);
const userData = ref({ ...props.user });

function handleSubmit() {
  emit("submit", userData.value);
  const modal = bootstrap.Modal.getInstance(
    document.getElementById("driverModal")
  );
  modal.hide();
}

function resetForm() {
  userData.value = { ...props.user };
}
</script>

<style>
.modal {
  z-index: 1050;
}
</style>
