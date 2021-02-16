<template>
  <Screen :progress="progress" class="trial">
    <template #0="{ responses }">
      <CategorizationMousetracking
        :select-event="'mouseover'"
        :response.sync="responses.response"
        :mouse-track.sync="responses.mouseTrack"
      >
        <template #option1>
          <div class="optionBox left">
            {{ leftOption }}
          </div>
        </template>
        <template #option2>
          <div class="optionBox right">
            {{ rightOption }}
          </div>
        </template>
        <template #stimulus>
          <Rsvp
            class="rsvp"
            :chunks="sentence.split(' ')"
            @end="rsvpDone = true"
          />
          <Wait
            v-if="rsvpDone"
            key="warning"
            :time="500"
            @done="displayWarning = $magpie.mousetracking.time.length <= 1"
          /><Wait
            key="mt-start"
            :time="0"
            @done="$magpie.mousetracking.start()"
          />
          <span v-if="displayWarning" class="exclamation-points">!!!</span>
        </template>
        <template #feedback>
          <p
            v-if="correctResponse"
            class="feedback"
            :style="{
              color:
                (responses.response === 'left' ? leftOption : rightOption) ===
                correctResponse
                  ? 'green'
                  : 'red'
            }"
          >
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
              $magpie.addTrialData({
                trialType,
                trialNumber,
                ...$magpie.currentTrial.training,
                ...responses.mouseTrack,
                response:
                  responses.response === 'left' ? leftOption : rightOption,
                left_box_is_option: !trueIsLeft ? 'falsch' : 'wahr',
                window_inner_height,
                window_inner_width,
                reaction_too_slow: displayWarning
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
      rsvpDone: false,
      window_inner_width: window.innerWidth,
      window_inner_height: window.innerHeight
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
  position: absolute;
  top: -29px;
}
.trial .optionBox {
  top: -49px;
}
.optionBox.left {
  left: -28px;
}
.optionBox.right {
  right: -28px;
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
