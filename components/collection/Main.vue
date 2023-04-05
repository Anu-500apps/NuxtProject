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
      <div>
        <div
          v-for="templates in templateData"
          :key="templates.name"
          class="border p-4 rounded-md mb-3 shadow-sm bg-white"
        >
          <section>
            <h5 class="font-[500] text-md mb-2">{{ templates.name }}</h5>
            <span class="font-[500] text-md mb-2">{{ templates.subject }}</span>
            <span class="font-[500] text-md mb-2 ml-4">{{
              templates.body
            }}</span>
          </section>
          <collectionList @edit="edit(templates)"></collectionList>
        </div>
      </div>
    </div>
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
              v-model="form.name"
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
              v-model="form.subject"
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
              v-model="form.body"
            />
          </div>
        </div>
        <div class="mt-6 flex items-center justify-end gap-x-6">
          <button
            type="button"
            class="text-sm font-semibold leading-6 text-gray-900"
            @click="form = ''"
          >
            Cancel
          </button>
          <button
            type="button"
            class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
            @click="submit()"
          >
            Save
          </button>
        </div>
      </div>
    </form>
  </div>
</template>
<script setup>
import { PhotoIcon, UserCircleIcon } from "@heroicons/vue/24/solid";
const propsect_data = ref([]);
const form = ref({
  project_id: "string",
  name: "",
  subject: "",
  body: "",
  is_active: "1",
  type: "HTML",
  share_type: "PRIVATE",
  category: "string",
});

// Get form
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
const submit = async () => {
  let options = {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
      Authorization:
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZDI1NjgxM2E2NjdjNDExM2ExZDBiNDY2NGI4YmRhNzUiLCJkIjoiMTY4MDA3OCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzY5MTR9.ESaiQVZYh45IyIJaP4A3YZO73FRLxd_lW1ATays2dhM",
    },
    body: JSON.stringify(form.value),
  };
  const { data: addTemplateData } = await useAuthLazyFetchPost(
    "https://v1-orm-lib.mars.hipso.cc/email-templates/",
    options
  );
  templateData.value.unshift(form.value);
  form.value = {};
};

// For Edit form
const edit = async (templates) => {
  form.value.name = templates.name;
  form.value.subject = templates.subject;
  form.value.body = templates.body;
  console.log("forrrrrrrrrrrrrrrrrrrrrrrrrrrrrr",form)
  //      let options = {
  //     method: "PUT",
  //     headers: {
  //       "Content-Type": "application/json",
  //       Accept: "application/json",
  //       Authorization:
  //         "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZDI1NjgxM2E2NjdjNDExM2ExZDBiNDY2NGI4YmRhNzUiLCJkIjoiMTY4MDA3OCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzY5MTR9.ESaiQVZYh45IyIJaP4A3YZO73FRLxd_lW1ATays2dhM",
  //     },
  //       body: form,
  //   };
  //  const { data: addTemplateData } = await useAuthLazyFetchPut(
  //     `"https://v1-orm-lib.mars.hipso.cc/email-templates/${form.id}"`,
  //     options
  //   );
  //   console.log("addTemplateData>>>>>>>>>.",addTemplateData)
};
// const post_call = (form) => {
//   template_data.value = form.template_name;
//   template_subject.value = form.subject;
//   template_text.value = form.text;
//   validate.value = false;
// };
// post_call();
</script>
