<template>
  <form>
    <div class="ml-4">
      <div class="mt-2">
        <div
          class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset sm:max-w-md"
        >
          <input
            type="text"
            name="website"
            id="website"
            class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
            placeholder="Enter Template Name"
            v-model="formData.name"
          />
        </div>
      </div>
      <div class="mt-2">
        <div
          class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset sm:max-w-md"
        >
          <input
            type="text"
            name="website"
            id="website"
            class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
            placeholder="Enter Subject"
            v-model="formData.subject"
          />
        </div>
      </div>

      <div>
        <div class="mt-2">
          <textarea
            rows="4"
            name="comment"
            id="comment"
            class="block w-full rounded-md border-0 text-black-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset sm:py-1.5 sm:text-sm sm:leading-6"
            placeholder="Add Template body............"
            v-model="formData.body"
          />
        </div>
      </div>
      <div class="mt-6 flex items-center justify-end gap-x-6">
        <button
          type="button"
          class="text-sm font-semibold leading-6 text-gray-900"
          @click="formData = ''"
        >
          Cancel
        </button>
        <button
          type="button"
          class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          @click="saveTemplate()"
        >
          Save
        </button>
      </div>
    </div>
  </form>
</template>
<script setup lang="ts">
// Define Emits Here
import { defineEmits } from "vue";
const emits = defineEmits(["submit-template"]);
const props = defineProps({
  // Declare props here
  formData: Object,
});

// Save Templats
const saveTemplate = async () => {
  let form = {
    project_id: "string",
    name: props.formData.name,
    subject: props.formData.subject,
    body: props.formData.body,
    is_active: "1",
    type: "HTML",
    share_type: "PRIVATE",
    category: "string",
  };
  // To assign uid to edit form
  if (props.formData && props.formData.uid) form["uid"] = props.formData.uid;
   emits("submit-template", form);
};
</script>
