<template>
  <q-page padding>
    <q-card class="">
      <q-card-section class="bg-light-blue-1">
        <div class="column row">
          <q-input v-model="mach" label="Enter Mach Number" suffix="[ ]" />
          <q-input v-model="gamma" label="Enter Gamma" suffix="[ ]" />
          <q-input v-model="p1" label="Enter Pressure (P1)" suffix="[MPa]" />

          <q-btn
            class="q-mt-md"
            icon="fas fa-calculator"
            label="Calculate"
            @click="calc"
            color="green"
          />
        </div>
      </q-card-section>
      <q-card-section class="bg-light-green-2">
        <div class="column row">
          <q-field label="Result (P2)" stack-label suffix="[MPa]">
            <template v-slot:control>
              <div class="self-center full-width no-outline" tabindex="0">
                {{ p2 | significant(3) }}
              </div>
            </template>
          </q-field>
        </div>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      mach: 1.2,
      gamma: 1.4,
      p1: 2,
      p2: 5
    };
  },

  methods: {
    myFunction() {
      return (
        1 + (2 * this.gamma * (this.mach * this.mach - 1)) / (this.gamma + 1)
      );
    },

    calc() {
      this.p2 = this.p1 * this.myFunction();
      //return this.p2
    }
  },
  filters: {
    significant: function(value, preicision) {
      if (value == null || value == false) {
        return "-";
      }

      return value.toPrecision(preicision);
    }
  }
};
</script>
<style lang="sass" scoped>
.my-card
  width: 500px
</style>
