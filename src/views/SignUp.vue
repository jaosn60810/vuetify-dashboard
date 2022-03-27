<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>Signup</h1>
        <v-form>
          <v-text-field type="email" label="Email"></v-text-field>

          <v-autocomplete
            label="Which browser do you use?"
            :items="browsers"
          ></v-autocomplete>

          <v-file-input label="Attach profile picture"></v-file-input>

          <v-text-field
            label="Birthday"
            v-model="birthday"
            readonly
          ></v-text-field>

          <v-date-picker v-model="birthday"></v-date-picker>

          <v-menu
            ref="menu"
            v-model="menu"
            :close-on-content-click="false"
            :return-value.sync="date"
            transition="scale-transition"
            offset-y
            min-width="auto"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                v-model="date"
                label="Picker in menu"
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker v-model="date" no-title scrollable>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="menu = false"> Cancel </v-btn>
              <v-btn text color="primary" @click="$refs.menu.save(date)">
                OK
              </v-btn>
            </v-date-picker>
          </v-menu>

          <v-checkbox label="Agree to terms & conditions"></v-checkbox>

          <v-btn type="submit" color=" primary">Submit</v-btn>
        </v-form>
      </v-col>
    </v-row></v-container
  >
</template>

<script>
export default {
  data() {
    return {
      browsers: ['Chrome', 'Firefox', 'Safari', 'Edge', 'Brave'],
      birthday: '',
      date: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
      menu: false,
      modal: false,
    };
  },
};
</script>

<style lang="scss" scoped></style>
