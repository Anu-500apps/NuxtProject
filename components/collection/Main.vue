<template>
  <div
    class="grid grid-rows-3 grid-flow-col grid-cols-4 border w-[80vw] mx-auto my-5 rounded-lg pr-[4px]"
  >
    <div
      class="row-span-3 bg-gray-50 border-r p-5 rounded-l-lg h-[calc(103vh-150px)] overflow-auto"
    >
      <div class="pb-3 w-[100%]">
        <button
          class="bg-white hover:bg-gray-50 hover:text-gray-800 border focus-visible:outline focus-visible:outline-2 focus-visible:outline-indigo-600 focus-visible:outline-offset-2 font-semibold inline-flex items-center justify-center px-3 py-3 rounded-md shadow-sm text-gray-600 text-sm w-[100%]"
          @click="validate = true"
        >
          Add Template
        </button>
      </div>
      <collectionList
        @edit-templates="editTemplats"
        @delete-templates="deleteTemplates"
        :templateData="templateData"
      ></collectionList>
    </div>
    <collectionAdd
      :formData="formsData"
      @submit-template="submitTemplate"
    ></collectionAdd>
  </div>
</template>
<script setup>
import { PhotoIcon, UserCircleIcon } from "@heroicons/vue/24/solid";
const propsect_data = ref([]);
const eamilIndex = ref(0);
const formsData = ref({
  name: "",
  subject: "",
  body: "",
});

// Get Email Templates
let options = {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Accept: "application/json",
    Authorization:
      "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZDI1NjgxM2E2NjdjNDExM2ExZDBiNDY2NGI4YmRhNzUiLCJkIjoiMTY4MDA3OCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzY5MTR9.ESaiQVZYh45IyIJaP4A3YZO73FRLxd_lW1ATays2dhM",
  },
};
const { data: templateData } = await useAuthLazyFetch(
  "https://v1-orm-lib.mars.hipso.cc/email-templates/?offset=0&limit=100&sort_column=id&sort_direction=desc"
);
// For add form
const submitTemplate = async (form) => {
console.log("updateTemplate(form);>>>>>>>",templateData)
  if (form.uid) return updateTemplate(form)
  let options = {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
      Authorization:
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZDI1NjgxM2E2NjdjNDExM2ExZDBiNDY2NGI4YmRhNzUiLCJkIjoiMTY4MDA3OCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzY5MTR9.ESaiQVZYh45IyIJaP4A3YZO73FRLxd_lW1ATays2dhM",
    },
    body: form,
  };
  const { data: addTemplateData } = await useAuthLazyFetchPost(
    "https://v1-orm-lib.mars.hipso.cc/email-templates/",
    options
  );
  templateData.value.unshift(form);
  formsData.value = {};
};
//For Edit form
const editTemplats = async (data, index) => {
  formsData.value = { ...data };
  eamilIndex.value = index;
};

// Updates templates after edit
const updateTemplate = async (form) => {
  let options = {
    method: "PUT",
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
      Authorization:
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZDI1NjgxM2E2NjdjNDExM2ExZDBiNDY2NGI4YmRhNzUiLCJkIjoiMTY4MDA3OCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzY5MTR9.ESaiQVZYh45IyIJaP4A3YZO73FRLxd_lW1ATays2dhM",
    },
    body: form,
  };
  const { data: addTemplateData } = await useAuthLazyFetchPut(
    `"https://v1-orm-lib.mars.hipso.cc/email-templates/${form.uid}"`,
    options
  );
  templateData.value[eamilIndex.value] = form;
  formsData.value = {};
};

// Delete Email Templates
const deleteTemplates = async (data,index) => {
  await useAuthLazyFetchDelete(
    `https://v1-orm-lib.mars.hipso.cc/email-templates/${data.uid}`,
  )
  templateData.value.splice(index, 1)
}
</script>
