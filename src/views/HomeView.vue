<template>
  <v-row justify="center">
    <h3>Leave a tip!</h3>
  </v-row>
  <v-container>
    <v-row justify="center">
      <v-col cols="4">
        <v-btn
          height="100"
          :color="btn1Color"
          block
          @click="toggleColor('btn1Color')"
          ><h1>20%</h1></v-btn
        >
      </v-col>
      <v-col cols="4">
        <v-btn
          height="100"
          :color="btn2Color"
          block
          @click="toggleColor('btn2Color')"
          ><h1>25%</h1></v-btn
        >
      </v-col>
      <v-col cols="4">
        <v-btn
          height="100"
          :color="btn3Color"
          block
          @click="toggleColor('btn3Color')"
          ><h1>80%</h1></v-btn
        >
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12">
        <v-dialog width="50%">
          <template v-slot:activator="{ props: activatorProps }">
            <v-btn
              v-bind="activatorProps"
              block
              color="blue"
              @click="dialog = true"
              ><h4>Custom</h4></v-btn
            >
          </template>
          <template v-slot:default="{ isActive }">
            <v-card>
              <v-card-title>
                <v-row justify="center">
                  <v-container> </v-container>
                  <span class="headline">Enter Custom Number</span>
                </v-row>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12">
                      <v-text-field
                        width="50%"
                        v-model="customNumber"
                        label="Custom Number"
                        type="number"
                        required
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-row>
                  <v-col cols="6">
                    <v-btn
                      block
                      color="blue darken-1"
                      text
                      @click="isActive.value = false"
                    >
                      Cancel
                    </v-btn>
                  </v-col>
                  <v-col cols="6">
                    <v-btn
                      color="blue darken-1"
                      text
                      block
                      @click="submitNumber, (isActive.value = false)"
                      >OK</v-btn
                    >
                  </v-col>
                </v-row>
              </v-card-actions>
            </v-card>
          </template>
        </v-dialog>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
// import { defineComponent } from "vue";
import { ref } from "vue";
import alertSoundFile from "@/assets/alarm.mp3";
import successSoundFile from "@/assets/success.mp3";
//Components
//import RouteCard from "@/components/cards/RouteCard.vue";
let alertSound = ref();
let successSound = ref();
alertSound.value = new Audio(alertSoundFile);
successSound.value = new Audio(successSoundFile);
let btn1Color = ref("blue");
let btn2Color = ref("blue");
let btn3Color = ref("blue");
const toggleColor = (refName) => {
  let buttonColor = eval(refName);
  console.log(buttonColor);
  let originalColor = buttonColor.value;
  if (refName != "btn3Color") {
    alertSound.value.play();
    buttonColor.value = buttonColor.value === "blue" ? "red" : "blue";
    setTimeout(() => {
      buttonColor.value = originalColor;
    }, 1000);
  } else {
    buttonColor.value = buttonColor.value === "blue" ? "green" : "blue";
    successSound.value.play();
    setTimeout(() => {
      buttonColor.value = originalColor;
    }, 1000);
  }
};
</script>

<style>
.topbtn {
}
</style>
