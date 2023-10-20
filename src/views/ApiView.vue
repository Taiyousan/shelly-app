<script setup>
import { ref, onMounted, toRaw } from "vue";
import axios from "axios";

const apiData = ref([]);
let displayData = ref(false);
let onOffToggle = ref(false); // true = on
let isOn = ref(false);

onMounted(async () => {
  const response = await axios.post(
    "https://shelly-86-eu.shelly.cloud/device/status",
    {
      id: "80646F827174",
      auth_key:
        "MWRmYzM2dWlkE62C6C4C76F817CE0A3D2902F5B5D4C115E49B28CF8539114D9246505DE5D368D560D06020A92480",
    },
    {
      headers: {
        "Content-Type": "application/x-www-form-urlencoded",
      },
    }
  );
  apiData.value = await response.data.data.device_status;
  onOffToggle.value = await response.data.data.device_status.relays[0].ison;
  console.log(toRaw(response));
});

// function async
async function switchPower(param) {
  console.log(param);
  const response = await axios.post(
    `"https://shelly-86-eu.shelly.cloud/relay/0?turn=${param}"`,
    {
      id: "80646F827174",
      auth_key:
        "MWRmYzM2dWlkE62C6C4C76F817CE0A3D2902F5B5D4C115E49B28CF8539114D9246505DE5D368D560D06020A92480",
    },
    {
      headers: {
        "Content-Type": "application/x-www-form-urlencoded",
      },
    }
  );
  apiData.value = await response.data.data.device_status;
  onOffToggle.value = await response.data.data.device_status.relays[0].ison;
  console.log(toRaw(response));
}
</script>

<template>
  <div class="api-results">
    <h2>Résultats de l'API</h2>
    <button @click="displayData = !displayData">
      {{
        displayData ? "Cacher le Device Status" : "Afficher le Device Status"
      }}
    </button>
    <ul v-if="displayData">
      <li v-for="(value, key) in apiData" :key="key">
        <strong>{{ key }}:</strong> {{ value }}
      </li>
    </ul>
    <div class="api-item temperature-item">
      {{ apiData.temperature }} degrés
      <div
        class="temperature"
        :style="{ width: apiData.temperature + '%' }"
      ></div>
    </div>
    <div class="api-item on-off-item">
      <div
        class="on-off-toggle"
        :class="{ 'on-toggle': onOffToggle, 'off-toggle': !onOffToggle }"
        @click="
          () => {
            onOffToggle = !onOffToggle;
            const param = onOffToggle ? 'on' : 'off';
            switchPower(param);
          }
        "
      >
        {{ onOffToggle ? "ON" : "OFF" }}
      </div>
    </div>
  </div>
</template>

<style scoped></style>
