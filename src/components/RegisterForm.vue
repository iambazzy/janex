<template>
  <v-form lazy-validation v-model="isValid" ref="register">
    <v-text-field
      dark
      type="text"
      color="white"
      label="First name"
      placeholder="Ex. Mohammad"
      outlined
      :rules="getRequiredRule('First name')"
    />

    <v-text-field
      dark
      type="text"
      color="white"
      label="Last name"
      placeholder="Ex. Basit"
      outlined
    />

    <v-text-field
      dark
      type="email"
      color="white"
      label="Email"
      placeholder="Ex. basit@gmail.com"
      :rules="getRequiredRule('Email')"
      outlined
    />

    <v-text-field
      dark
      type="password"
      color="white"
      label="Password"
      placeholder="Enter your password"
      hint="At least 8 characters long"
      :rules="getRequiredRule('Password')"
      outlined
    />

    <div
      class="file-uploader py-6 d-flex flex-column justify-center align-center"
    >
      <input
        type="file"
        ref="fileInput"
        hidden
        multiple
        @change="handleChangeInFileUpload"
      />

      <div @click="upload" class="d-flex flex-column">
        <v-icon color="white">mdi-cloud-upload</v-icon>
        <v-btn text color="white" small>
          {{ filesUploaded.length ? "Upload more" : "Upload Files" }}
        </v-btn>
      </div>

      <v-expand-transition>
        <div v-show="filesUploaded.length">
          <v-menu
            v-model="menu"
            :close-on-content-click="false"
            :nudge-top="nudgeTop"
            :nudge-left="nudgeLeft"
            offset-x
            left
          >
            <template v-slot:activator="{ on, attrs }" class="mt-0">
              <v-chip
                class="menu-btn black--text mt-2"
                color="white"
                v-bind="attrs"
                v-on="on"
                small
              >
                View files ({{ filesUploaded.length }})
              </v-chip>
            </template>

            <v-card width="350px">
              <v-card-text class="files-holder">
                <h4 class="mb-2">{{ filesUploaded.length }} files uploaded.</h4>
                <div
                  v-for="(file, index) in filesUploaded"
                  :key="index"
                  class="d-flex align-center justify-space-between mb-2"
                >
                  <div>{{ file.name | trimFileName }}</div>

                  <v-btn
                    depressed
                    x-small
                    icon
                    color="red"
                    class="white--text ml-3"
                    @click="removeFile(file)"
                  >
                    <v-icon>mdi-delete</v-icon>
                  </v-btn>
                </div>
              </v-card-text>
            </v-card>
          </v-menu>
        </div>
      </v-expand-transition>
    </div>

    <v-btn
      color="white"
      class="mt-6"
      outlined
      depressed
      block
      large
      @click="register"
    >
      Create account <v-icon class="pl-3">mdi-arrow-right</v-icon>
    </v-btn>
  </v-form>
</template>

<script>
export default {
 data() {
  return {
   menu: false,
   isValid: false,
   backup: [],
   filesUploaded: []
  }
 },

 filters: {
  trimFileName(val) {
   if (val.length > 50) return val.slice(0, 25) + '...';
   return val;
  }
 },

 computed: {
  getRequiredRule() {
   return (type) => {
    return [(value) => !!value || `${type} is required`]
   }
  },
  nudgeTop() {
   return this.$vuetify.breakpoint.mdAndUp ? 85 : 205;
  },
  nudgeLeft() {
   return this.$vuetify.breakpoint.mdAndUp ? 195 : ''
  }
 },

 methods: {
  register() {
   if (!this.$refs.register.validate()) return;
  },

  upload() {
   this.$refs.fileInput.click();
  },

  handleChangeInFileUpload({ target }) {
   this.filesUploaded = [...this.filesUploaded, ...target.files];
  },

  removeFile(file) {
   this.filesUploaded = this.filesUploaded.filter(el => el.name !== file.name);
   if (this.filesUploaded.length === 0) this.menu = false;
  }
 }
}
</script>

<style scoped lang="scss">
.menu-btn {
  margin-top: -2px;
}

.file-uploader {
  position: relative;
  border: 1px dotted white;
  border-radius: 5px;
}

.files-holder {
  max-height: 250px;
  overflow: auto;
}
</style>