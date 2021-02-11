<template>
  <!--
  Set your experiment id here and
  Define your data sources with the trials attribute -->
  <Experiment
    title="2Step-SI Online Studie"
    :trials="{
      training,
      test
    }"
    :wide="true"
  >
    <!-- The contents of the #title template slot will be displayed in the upper left corner of the experiment -->
    <template #title>
      <div></div>
    </template>

    <!-- The contents of the #screens template slot define your experiment -->
    <template #screens>
      <Screen
        :title="'Probandeninformation zur Studie “2Step-SI”'"
        class="instructions"
      >
        <Instructions />
        <br />
        <!-- The $magpie field gives you access to magpie-specific functionality -->
        <button @click="$magpie.nextScreen">Weiter</button>
      </Screen>

      <Screen
        :title="'Hinweise zur Durchführung dieses Versuchs'"
        class="instructions"
      >
        <p>
          Bitte benutzen Sie für die Dauer des Experimentes den "Fullscreen
          Modus":
          <a href="javascript:void(0)" @click="turnOnFullScreen"
            >Auf Fullscreen umschalten</a
          >
        </p>
        <p>Benutzen Sie eine Maus oder ein Trackpad.</p>
        <p>
          Wenn Sie eine Maus benutzen, schaffen Sie sich Platz für die
          Mausbewegung. Sie sollten den Mauszeiger in einer Bewegung ohne
          Abheben der Maus von der unteren zur oberen Bildschirmkannte bewegen
          können.
        </p>
        <p>
          Als nächstes folgen einige Probedurchgänge zur Benutzung von Maus oder
          Trackpad. Bitte folgen Sie den Anweisungen auf dem Bildschirm.
        </p>
        <br />
        <!-- The $magpie field gives you access to magpie-specific functionality -->
        <button @click="$magpie.nextScreen">Weiter</button>
      </Screen>

      <template v-for="i in 6">
        <Screen :key="'mouse_speed_test-' + i">
          <template #0="{ responses }">
            Klicken Sie auf "go" und bewegen Sie die Maus so schnell wie möglich
            in einer geraden Linie auf die graue Box.
            <CategorizationMousetracking
              :select-event="'mouseover'"
              :mouse-track.sync="responses.mouseTrack"
            >
              <template #option1>
                <div v-if="i % 2 === 0" class="optionBox">
                  X
                </div>
              </template>
              <template #option2>
                <div v-if="i % 2 === 1" class="optionBox">
                  X
                </div>
              </template>
              <template #stimulus>
                <Timer key="mouse-time" v-model="responses.timer" />
                <Wait
                  key="mt-start"
                  :time="0"
                  @done="$magpie.startMouseTracking()"
                />
              </template>
              <template #feedback>
                <Wait
                  :time="0"
                  @done="
                    $magpie.addResult({
                      trialType: 'mouse-speed-test',
                      trialNumber: i,
                      ...$magpie.currentTrial.training,
                      ...responses.mouseTrack,
                      ...getScreenDimensions(),
                      position: i % 2 === 0 ? 'left' : 'right',
                      mouse_speed_time: responses.timer()
                    });
                    $magpie.nextScreen();
                  "
                />
              </template>
            </CategorizationMousetracking>
          </template>
        </Screen>
      </template>

      <Screen :title="'Instruktionen'" class="instructions">
        <Instructions2 />
        <button @click="$magpie.nextScreen">Trainingsphase starten</button>
      </Screen>

      <!-- Practice trials -->
      <!-- Here we create screens in a loop for every entry in training -->
      <template v-for="i in 5">
        <TrialScreen
          :key="'training-' + i"
          :trial-type="'training'"
          :trial-number="i"
          :sentence="$magpie.currentTrial.training.stimulus"
          :group="groupName"
          :correct-response="getCorrectResponse()"
          :true-is-left="lr === 1"
          :progress="(i - 1) / 5"
        />
      </template>

      <Screen :title="'Kurze Pause!'">
        Das Training ist vorbei. Nehmen Sie sich gerne eine kurze Pause, bevor
        Sie mit dem Hauptteil des Experiments beginnen.
        <button @click="$magpie.nextScreen">
          Zum Hauptteil des Experiments
        </button>
      </Screen>

      <template v-for="i in 5">
        <TrialScreen
          :key="'test-' + i"
          :trial-type="'main'"
          :trial-number="i"
          :sentence="$magpie.currentTrial.test.stimulus"
          :group="groupName"
          :true-is-left="lr === 1"
          :progress="(i - 1) / 5"
        />
      </template>

      <Screen>
        <template #0="{responses}">
          <p>What did you use to complete this task?</p>
          <ForcedChoiceInput
            :response.sync="responses.inputmethod"
            :options="['Mouse', 'Trackpad', 'both']"
          />
        </template>
      </Screen>

      <DebugResults />

      <!-- While developing your experiment, using the DebugResults screen is fine,
      once you're going live, you can use the <SubmitResults> screen to automatically send your experimental data to the server. -->

      <Screen :title="'Thanks!'">
        Goodbye
      </Screen>
    </template>
  </Experiment>
</template>

<script>
// Load data from csv files as javascript arrays with objects
import test from '../trials/test.csv';
import training from '../trials/training.csv';
import _ from 'lodash';
import TrialScreen from './TrialScreen.vue';
import Instructions from './Instructions';
import Instructions2 from './Instructions2';

export default {
  name: 'App',
  components: { Instructions, TrialScreen, Instructions2 },
  data() {
    console.log(training);
    const group = Math.round(Math.random());
    const lr = Math.round(Math.random());
    return {
      group,
      lr,
      test: _.shuffle(test),
      test_length: test.length,
      training: _.shuffle(training),
      training_length: training.length
    };
  },
  computed: {
    groupName() {
      return this.group === 0 ? 'semantic' : 'pragmatic';
    },
    groupCorrectResponse() {
      return this.group === 0 ? 'w' : 'f';
    }
  },
  methods: {
    getCorrectResponse() {
      return this.$magpie.currentTrial.training.type !== 'Some critical'
        ? this.$magpie.currentTrial.training['correct.response']
        : this.groupCorrectResponse;
    },
    async turnOnFullScreen() {
      if (!document.fullscreenElement) {
        try {
          await document.documentElement.requestFullscreen();
          return true;
        } catch (e) {
          return false;
        }
      }
      return true;
    },
    turnOffFullScreen() {
      document.exitFullscreen();
    },
    getScreenDimensions() {
      return {
        window_inner_width: window.innerWidth,
        window_inner_height: window.innerHeight
      };
    }
  }
};
</script>
<style>
.instructions {
  text-align: left;
}
</style>
