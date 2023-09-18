<template>
  <div class="w-full h-[852px] p-4 relative bg-neutral-50">
    <form
      class="w-full h-full flex flex-col gap-4 relative"
      @submit.prevent="submitForm"
    >
      <div class="self-stretch justify-between items-center gap-2 inline-flex">
        <div
          class="pl-2 pr-4 py-2 bg-[#ededed] rounded-[100px] justify-start items-center gap-2 flex cursor-pointer hover:bg-white"
          @click="gotoPre"
        >
          <div class="w-6 h-6 relative">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
            >
              <path
                d="M6.65005 12.35L12.5 18.2L12 18.7L5.30005 12L12 5.29999L12.5 5.79999L6.65005 11.65H18.7V12.35H6.65005Z"
                fill="black"
              />
            </svg>
          </div>
          <div class="text-black text-base font-normal">Abbrechen</div>
        </div>
        <button
          class="px-4 py-2 bg-[#ededed] rounded-[100px] justify-start items-center gap-2 flex cursor-pointer text-black text-base font-normal hover:bg-white"
          @click.prevent="submitForm"
          type="submit"
        >
          Speichern
        </button>
      </div>
      <div class="self-stretch h-7 justify-start items-start gap-2 inline-flex">
        <div class="grow shrink basis-0 text-zinc-800 text-2xl font-bold">
          #12832
        </div>
      </div>
      <div
        class="self-stretch h-fit flex-col justify-start items-start gap-4 flex"
      >
        <div
          class="self-stretch px-4 py-2 bg-[#ededed] rounded-[100px] justify-center items-center gap-2 inline-flex"
        >
          <div
            class="w-2/6 sm:w-1/6 text-black text-opacity-75 py-3 text-xs font-bold"
          >
            Patient:
          </div>
          <v-autocomplete
            class="w-4/6 sm:w-5/6"
            :items="this.patientNames"
            item-title="name"
            item-value="id"
            variant="outlined"
            hide-details
            v-model="selectedPatientId"
          >
          </v-autocomplete>
        </div>
        <div
          class="self-stretch px-4 py-2 bg-[#ededed] rounded-[100px] justify-center items-center gap-2 inline-flex"
        >
          <div
            class="w-2/6 sm:w-1/6 text-black text-opacity-75 py-3 text-xs font-bold"
          >
            Zahnartzt:
          </div>
          <v-autocomplete
            class="w-4/6 sm:w-5/6"
            :items="this.dentistNames"
            item-title="name"
            item-value="id"
            variant="outlined"
            hide-details
            v-model="selectedDentistId"
          ></v-autocomplete>
        </div>
        <div
          class="self-stretch px-4 py-2 bg-[#ededed] rounded-[100px] justify-center items-center gap-2 inline-flex"
        >
          <div
            class="w-2/6 sm:w-1/6 text-black text-opacity-75 py-3 text-xs font-bold"
          >
            Dienstleister:
          </div>
          <v-autocomplete
            class="w-4/6 sm:w-5/6"
            :items="this.locationNames"
            item-title="name"
            item-value="id"
            variant="outlined"
            hide-details
            v-model="selectedLocationId"
          ></v-autocomplete>
        </div>
        <div
          class="self-stretch px-4 py-2 bg-[#ededed] rounded-[100px] justify-center items-center gap-2 inline-flex"
        >
          <div
            class="w-2/6 sm:w-1/6 text-black text-opacity-75 py-3 text-xs font-bold"
          >
            Standort:
          </div>
          <v-autocomplete
            class="w-4/6 sm:w-5/6"
            :items="this.serviceNames"
            item-title="name"
            item-value="id"
            variant="outlined"
            hide-details
            v-model="selectedServiceId"
          ></v-autocomplete>
        </div>
        <div
          class="self-stretch px-4 py-2 bg-[#ededed] rounded-[100px] justify-center items-center gap-2 inline-flex"
        >
          <div
            class="w-2/6 sm:w-1/6 py-3 text-black text-opacity-75 text-xs font-bold"
          >
            Rd zu Bp:
          </div>
          <input
            class="w-4/6 sm:w-5/6 grow shrink basis-0 bg-[#ededed] h-full px-2 text-sm font-normal"
            v-model="rd_to_bp"
            type="date"
          />
        </div>
        <div
          class="self-stretch h-fit px-4 py-3 bg-[#ededed] rounded-lg flex-col justify-center items-center gap-2 flex"
        >
          <div
            class="self-stretch text-black text-opacity-75 text-xs font-bold"
          >
            Arbeitsbeschreibung:
          </div>
          <textarea
            class="bg-[#ededed] w-full h-16 p-2 text-sm font-normal"
            v-model="work_details"
            type="text"
            placeholder="Hier eintreten..."
          ></textarea>
        </div>
        <div
          class="self-stretch h-[104px] px-4 py-2 bg-[#ededed] rounded-lg flex-col justify-start items-start gap-2 flex"
          @dragenter.prevent
          @dragover.prevent
          @drop="handleFileDrop"
        >
          <input
            type="file"
            ref="fileInput"
            style="display: none"
            @change="handleFileUpload"
          />
          <div
            class="self-stretch justify-start items-center gap-2 inline-flex"
          >
            <div
              class="grow shrink basis-0 text-black text-opacity-75 text-xs font-bold"
            >
              Eingereichte Unterlagen:
            </div>
            <div
              class="w-6 h-6 relative bg-white rounded-2xl cursor-pointer"
              @click="openFile"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
              >
                <rect width="24" height="24" rx="12" fill="white" />
                <path
                  d="M11.65 12.35H6.30005V11.65H11.65V6.3H12.35V11.65H17.7V12.35H12.35V17.7H11.65V12.35Z"
                  fill="black"
                />
              </svg>
            </div>
          </div>
          <div
            class="self-stretch p-4 opacity-25 justify-center items-center gap-2 inline-flex"
          >
            <div class="w-6 h-6 relative">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="25"
                height="24"
                viewBox="0 0 25 24"
                fill="none"
              >
                <path
                  d="M7.00005 18.7C5.83338 18.7 4.84172 18.2936 4.02505 17.4807C3.20838 16.6678 2.80005 15.6742 2.80005 14.5C2.80005 13.35 3.21255 12.3625 4.03755 11.5375C4.86255 10.7125 5.80005 10.3 6.85005 10.3C7.01672 8.86667 7.63755 7.675 8.71255 6.725C9.78755 5.775 11.05 5.3 12.5 5.3C14.0879 5.3 15.4349 5.85304 16.5409 6.9591C17.647 8.06519 18.2 9.41215 18.2 11V12.3H19C19.9 12.3 20.6584 12.6083 21.275 13.225C21.8917 13.8417 22.2 14.6 22.2 15.5C22.2 16.4 21.9 17.1583 21.3 17.775C20.7 18.3917 19.95 18.7 19.05 18.7H13.65C13.2167 18.7 12.8584 18.5583 12.575 18.275C12.2917 17.9917 12.15 17.6333 12.15 17.2V11.2L9.90005 13.45L9.40005 12.975L12.5 9.875L15.6 12.975L15.1 13.45L12.85 11.2V17.2C12.85 17.4 12.9334 17.5833 13.1 17.75C13.2667 17.9167 13.45 18 13.65 18H19C19.7 18 20.2917 17.7583 20.775 17.275C21.2584 16.7917 21.5 16.2 21.5 15.5C21.5 14.8 21.2584 14.2083 20.775 13.725C20.2917 13.2417 19.7 13 19 13H17.5V11C17.5 9.61667 17.0125 8.4375 16.0375 7.4625C15.0625 6.4875 13.8834 6 12.5 6C11.1167 6 9.93755 6.4875 8.96255 7.4625C7.98755 8.4375 7.50005 9.61667 7.50005 11H6.95005C6.03338 11 5.22922 11.3417 4.53755 12.025C3.84588 12.7083 3.50005 13.5333 3.50005 14.5C3.50005 15.4667 3.84172 16.2917 4.52505 16.975C5.20838 17.6583 6.03338 18 7.00005 18H9.50005V18.7H7.00005Z"
                  fill="black"
                />
              </svg>
            </div>
            <div
              v-if="uploadedFile"
              class="text-blue-700 font-bold text-base sm:text-lg"
            >
              {{ uploadedFile.name }} uploaded
            </div>
            <div v-else class="text-black text-sm font-bold">
              Hier hochladen
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'CreateComponent',

  data() {
    return {
      patientData: null,
      dentistData: null,
      locationData: null,
      serviceData: null,
      dentistNames: [],
      patientNames: [],
      locationNames: [],
      serviceNames: [],
      loading: false,
      patient: null,
      dentist: null,
      service_provider: null,
      location: null,
      rd_to_bp: null,
      work_details: null,
      uploadedFile: null,

      selectedPatientId: null,
      selectedDentistId: null,
      selectedLocationId: null,
      selectedServiceId: null,
    };
  },

  async created() {
    this.loading = true;
    const runtimeConfig = useRuntimeConfig();

    try {
      const [
        patientResponse,
        dentistResponse,
        locationResponse,
        serviceResponse,
      ] = await Promise.all([
        fetch('https://app.wunschlachen.de/staging/items/patients', {
          method: 'GET',
          headers: {
            Authorization: runtimeConfig.public.BEARER_TOKEN,
          },
        }),
        fetch('https://app.wunschlachen.de/staging/items/dentists', {
          method: 'GET',
          headers: {
            Authorization: runtimeConfig.public.BEARER_TOKEN,
          },
        }),
        fetch('https://app.wunschlachen.de/staging/items/locations', {
          method: 'GET',
          headers: {
            Authorization: runtimeConfig.public.BEARER_TOKEN,
          },
        }),
        fetch('https://app.wunschlachen.de/staging/items/service_provider', {
          method: 'GET',
          headers: {
            Authorization: runtimeConfig.public.BEARER_TOKEN,
          },
        }),
      ]);

      // Processing patientResponse
      if (patientResponse.ok) {
        this.patientData = await patientResponse.json();
        this.patientNames = this.patientData.data.map((item) => {
          return {
            name: `${item.first_name}, ${item.last_name}`,
            id: item.id,
          };
        });
      } else {
        console.error('Response Error:', patientResponse);
      }

      // Processing dentistResponse
      if (dentistResponse.ok) {
        this.dentistData = await dentistResponse.json();
        this.dentistNames = this.dentistData.data.map((item) => {
          return {
            name: `${item.first_name}, ${item.last_name}`,
            id: item.id,
          };
        });
      } else {
        console.error('Response Error:', dentistResponse);
      }

      // Processing locationResponse
      if (locationResponse.ok) {
        this.locationData = await locationResponse.json();
        this.locationNames = this.locationData.data.map((item) => {
          return {
            name: `${item.name}`,
            id: item.id,
          };
        });
      } else {
        console.error('Response Error:', locationResponse);
      }

      // Processing patientResponse
      if (serviceResponse.ok) {
        this.serviceData = await serviceResponse.json();
        this.serviceNames = this.serviceData.data.map((item) => {
          return {
            name: `${item.first_name}, ${item.last_name}`,
            id: item.id,
          };
        });
      } else {
        console.error('Response Error:', serviceResponse);
      }
    } catch (error) {
      console.error('Fetch error:', error);
    } finally {
      this.loading = false;
    }
  },

  methods: {
    gotoPre() {
      this.$emit('changeComponent', 'ListComponent');
    },

    openFile() {
      this.$refs.fileInput.click();
    },

    handleFileUpload(e) {
      // When a file is selected...
      const files = e.target.files || e.dataTransfer.files;
      if (!files.length) return;
      this.createFile(files[0]);
    },

    handleFileDrop(e) {
      // When a file is dropped...
      this.handleFileUpload(e);
    },

    createFile(file) {
      // This is where you can handle the uploaded file.
      // For example, upload to a server using an AJAX method.
      console.log(file);
      this.uploadedFile = file;
    },

    async submitForm() {
      // data to be sent
      const formData = {
        patient: this.selectedPatientId,
        dentist: this.selectedDentistId,
        service_provider: this.selectedServiceId,
        location: this.selectedLocationId,
        rd_to_bp: this.rd_to_bp,
        work_details: this.work_details,
        // assuming you have a field for storing the file id
        files: this.uploadedFile ? this.uploadedFile.id : null,
      };

      try {
        const runtimeConfig = useRuntimeConfig();
        const response = await fetch(
          'https://app.wunschlachen.de/staging/items/Laboratory_work',
          {
            method: 'POST',
            headers: {
              Authorization: runtimeConfig.public.BEARER_TOKEN,
            },
            body: formData,
          }
        );

        // Use fetch API to make a POST request
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }

        const data = await response.json();
        console.log('response = ', data);
      } catch (error) {
        console.error('An error occurred:', error);
      }
    },
  },
};
</script>
