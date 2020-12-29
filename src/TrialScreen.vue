<template>
  <Screen :progress="progress">
    <template #0="{ responses }">
      <CategorizationMousetracking
        :select-event="'click'"
        :response.sync="responses.response"
        :mouse-track.sync="responses.mouseTrack"
      >
        <template #option1>
          <div class="optionBox">
            {{ leftOption }}
          </div>
        </template>
        <template #option2>
          <div class="optionBox">
            {{ rightOption }}
          </div>
        </template>
        <template #stimulus>
          <Rsvp
            class="rsvp"
            :chunks="sentence.split(' ')"
            @end="
              $magpie.startMouseTracking();
              rsvpDone = true;
            "
          />
          <Wait
            v-if="rsvpDone"
            key="warning"
            :time="500"
            @done="displayWarning = $magpie.mousetrackingTime.length <= 1"
          />
          <span v-if="displayWarning" class="exclamation-points">!!!</span>
        </template>
        <template #feedback>
          <p v-if="correctResponse" class="feedback">
            {{
              (responses.response === 'left' ? leftOption : rightOption) ===
              correctResponse
                ? 'korrekt'
                : 'inkorrekt'
            }}
          </p>
          <Wait
            :time="1000"
            @done="
              $magpie.addResult({
                trialType,
                trialNumber,
                ...$magpie.currentTrial.training,
                ...responses.mouseTrack,
                response:
                  responses.response === 'left' ? leftOption : rightOption,
                group,
                left_box_is_option: !trueIsLeft ? 'falsch' : 'wahr'
              });
              $magpie.nextScreen();
            "
          />
        </template>
      </CategorizationMousetracking>
    </template>
  </Screen>
</template>
<script>
export default {
  name: 'TrialScreen',
  props: {
    trialType: {
      type: String,
      required: true
    },
    trialNumber: {
      type: Number,
      required: true
    },
    sentence: {
      type: String,
      required: true
    },
    trueIsLeft: {
      type: Boolean,
      required: true
    },
    correctResponse: {
      type: String,
      default: ''
    },
    group: {
      type: String,
      required: true
    },
    progress: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      displayWarning: false,
      rsvpDone: false
    };
  },
  computed: {
    leftOption() {
      return !this.trueIsLeft ? 'f' : 'w';
    },
    rightOption() {
      return !this.trueIsLeft ? 'w' : 'f';
    }
  }
};
</script>
<style>
.optionBox {
  width: 90px;
  height: 90px;
  box-sizing: border-box;
  padding: 30px;
  background-color: lightgray;
  font-size: 30px;
}

.rsvp {
  font-size: 40px;
}

.exclamation-points {
  color: darkred;
  font-size: 100px;
}

.feedback {
  font-size: 50px;
}
</style>
