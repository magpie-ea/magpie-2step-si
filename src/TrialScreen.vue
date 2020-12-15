<template>
  <CategorizationMousetracking>
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
      <Rsvp :chunks="sentence.split(' ')" @end="$magpie.startMouseTracking()" />
    </template>
    <template #feedback="{mouseTrack, label}">
      <p v-if="correctResponse">
        {{ (label === 'left'? leftOption : rightOption) == correctResponse? 'korrekt' : 'inkorrekt'}}
      </p>
      <Wait :time="500" @done="$magpie.addResult({
        ...$magpie.currentTrial.training,
        ...mouseTrack,
        response: (label === 'left'? leftOption : rightOption),
        group,
        left_box_is_option: !trueIsLeft? 'falsch' : 'wahr',
      });
      $magpie.nextScreen()" />
    </template>

  </CategorizationMousetracking>
</template>
<script>
export default {
  name: 'TrialScreen',
  props: {
    sentence: {
      type: String,
      required: true,
    },
    trueIsLeft: {
      type: Boolean,
      required: true,
    },
    correctResponse: {
      type: String,
      default: '',
    },
    group: {
      type: String,
      required: true,
    }
  },
  computed: {
    leftOption() {
      return !this.trueIsLeft? 'f' : 'w'
    },
    rightOption() {
      return !this.trueIsLeft? 'w' : 'f'
    }
  }
};
</script>
<style>
.optionBox {
  width: 60px;
  height: 60px;
  box-sizing: border-box;
  padding: 20px;
  background-color: lightyellow;
}
</style>
