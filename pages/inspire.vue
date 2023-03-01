<template>
  <v-container>
    <v-row>
      <v-col>Date</v-col>
      <v-col>
        <v-menu
          ref="date1StartMenu"
          v-model="date1.start.menu"
          min-width="auto"
          offset-y
          transition="scale-transition"
          :close-on-content-click="false"
          :return-value.sync="date1.start.value"
        >
          <template v-slot:activator="{ attrs, on }">
            <v-text-field
              v-model="date1.start.value"
              label="Start"
              prepend-inner-icon="mdi-calendar"
              outlined
              readonly
              v-bind="attrs"
              v-on="on"
            >
            </v-text-field>
          </template>
          <v-date-picker v-model="date1.start.value" no-title scrollable>
            <v-spacer></v-spacer>
            <v-btn text color="primary" @click="date1.start.menu = false"> Cancel </v-btn>
            <v-btn
              text
              color="primary"
              @click="$refs.date1StartMenu.save(date1.start.value)"
            >
              OK
            </v-btn>
          </v-date-picker>
        </v-menu>
      </v-col>
      <v-col>
        <v-menu
          ref="date1EndMenu"
          v-model="date1.end.menu"
          min-width="auto"
          offset-y
          transition="scale-transition"
          :close-on-content-click="false"
          :return-value.sync="date1.start.value"
        >
          <template v-slot:activator="{ attrs, on }">
            <v-text-field
              v-model="date1.end.value"
              label="End"
              prepend-inner-icon="mdi-calendar"
              outlined
              readonly
              v-bind="attrs"
              v-on="on"
            >
            </v-text-field>
          </template>
          <v-date-picker
            v-model="date1.end.value"
            no-title
            scrollable
            :allowed-dates="date1EndAllowedDates"
          >
            <v-spacer></v-spacer>
            <v-btn text color="primary" @click="date1.end.menu = false"> Cancel </v-btn>
            <v-btn text color="primary" @click="$refs.date1EndMenu.save(date1.end.value)">
              OK
            </v-btn>
          </v-date-picker>
        </v-menu>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      date1: {
        start: {
          menu: false,
          value: new Date().toISOString().substr(0, 10),
        },
        end: {
          allowedDates: [],
          menu: false,
          value: null,
        },
      },
    };
  },
  methods: {
    date1EndAllowedDates(value) {
      return this.date1.end.allowedDates.includes(value);
    },
  },
  watch: {
    "date1.start.value": function (value) {
      const firstDateOfMonth = this.$moment(value).format("YYYY-MM-DD");

      const lastDateOfMonth = this.$moment(value).add(12, "weeks").format("YYYY-MM-DD");

      const endAllowedDates = [];

      const twixDays = this.$moment
        .twix(new Date(firstDateOfMonth), new Date(lastDateOfMonth))
        .iterate("days");

      while (twixDays.hasNext()) {
        endAllowedDates.push(twixDays.next().format("YYYY-MM-DD"));
      }

      this.date1.end.allowedDates = endAllowedDates;
    },
  },
};
</script>
