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
        <p>
          Sie beteiligen sich an einer psycholinguistischen Studie des Instituts
          für Kognitionswissenschaft der Universität Osnabrück, Fachgebiet
          Kognitive Modellierung, Projektleitung Prof. Dr. Michael Franke.
        </p>
        <h2>Hintergrund und Ziel der Studie</h2>
        <p>
          In der vorliegenden Studie soll untersucht werden, wie
          Sprachinterpretation in kurzer Zeit und womöglich unbewusst zustande
          kommt.
        </p>
        <h2>Versuchsablauf</h2>
        <p>
          Das Experiment wird insgesamt etwa 20-25 Minuten in Anspruch nehmen
          und besteht aus einer Übungsphase, die Sie an die Bedienung des
          Experiments und Ihre Aufgabe heranführt, sowie der eigentlichen
          Testphase.
        </p>
        <p>
          Im folgenden Experiment werden Sie gebeten, einfache deutsche Sätze
          auf ihren Wahrheitswert zu überprüfen. Das heißt: Ihnen wird jeweils
          ein Satz schriftlich präsentiert und Ihre Aufgabe ist es zu
          entscheiden, ob es sich um einen wahren oder einen falschen Satz
          handelt. Die folgenden beiden Beispielsätze veranschaulichen diese
          Aufgabe:
        </p>
        <ol>
          <li>
            »Alle Hunde sind Säugetiere.« Ist dieser Satz wahr oder falsch?
          </li>
          <li>
            »Einige Möbel sind Zitronen.« Ist dieser Satz wahr oder falsch?
          </li>
        </ol>
        <p>
          Sie steuern hierbei den zeitlichen Ablauf des Experiments selbst, es
          gibt also keinen Zeitdruck für Sie. Sie können jederzeit eine kleine
          Pause einlegen, etwa um Ihre Sitz- oder Armposition zu justieren oder
          um Nachfragen zu stellen.
        </p>
        <p>
          Die Sätze, die Sie in diesem Experiment lesen werden, sind allesamt
          unverfänglich. Es sind keine Risiken der Teilnahme zu erwarten.
        </p>
        <h2>Was wird gemessen?</h2>
        <p>
          Während der Testphase des Experiments zeichnen wir ihre Antworten
          (wahr/falsch) auf, die Zeit, die Sie sich zum Antworten genommen
          haben, sowie die Bewegung der Maus hin zur gewählten Antwort.
        </p>
        <h2>Sicherheitshinweis</h2>
        <p>
          Sie werden gebeten, bei körperlichem oder psychischem Unwohlsein
          unverzüglich den Versuch abzubrechen. Hierdurch entstehen für Sie
          keine Nachteile.
        </p>
        <h2>
          Freiwillige Teilnahme, Umgang mit Ihren Daten, Aufwandsentschädigung
        </h2>
        <p>
          Sie können Ihre Teilnahme jederzeit und ohne Angabe von Gründen
          abbrechen.
        </p>
        <p>
          Die Versuchsleitung verpflichtet sich Ihnen gegenüber, die gewonnenen
          Daten pseudonymisiert zu behandeln und Dritten eine Zuordnung Ihrer
          Person zu den Daten nicht zu ermöglichen. Ihre letztlich vollständig
          anonymisierten Daten werden nur zu Forschungszwecken gespeichert und
          verwertet. Erfasste Primärdaten werden gemäß den Empfehlungen der
          Deutschen Forschungsgemeinschaft (DFG) für mindestens 10 Jahre nach
          der Datenerhebung aufbewahrt.
        </p>
        <p>
          Es ist geplant, die Daten und Ergebnisse dieser Studie als
          wissenschaftliche Publikation zu veröffentlichen. Dies geschieht in
          anonymisierter Form, d. h. ohne dass die Daten einer bestimmten Person
          zugeordnet werden können. Die vollständig anonymisierten Daten dieser
          Studie sollen zudem als offene Daten im Internet in einem Datenarchiv
          (voraussichtlich osf.org) zugänglich gemacht werden. Damit folgt diese
          Studie den Empfehlungen der Deutschen Forschungsgemeinschaft (DFG) und
          der Deutschen Gesellschaft für Psychologie (DGPs) zur
          Qualitätssicherung in der Forschung. Ein solches Vorgehen bedeutet,
          dass auch andere Forscherinnen und Forscher auf die anonymisierten
          Daten zugreifen können, um diese ggf. neu auszuwerten und
          weiterführende eigene Fragestellungen zu untersuchen.
        </p>
        <p>
          Sie können Ihre Einwilligung zur Speicherung der Daten bis zum Ende
          der Datenerhebung widerrufen, ohne dass Ihnen daraus Nachteile
          entstehen. Nach Abschluss der Erhebung und der dann folgenden
          Anonymisierung der Daten ist der Einspruch nicht mehr möglich.
        </p>
        <p>
          Studierende des Bachelorstudiengangs <i>Cognitive Science</i> erhalten
          eine Bestätigung über die Teilnahme an einem psychologischen
          Experiment im Umfang von einer Versuchspersonenstunde bei Abschluss
          des Experiments. Diese steht Ihnen zu, sobald Sie mit dem Experiment
          beginnen, auch wenn Sie das Experiment vor Beendigung abrechen müssen,
          aus welchen Gründen auch immer. Auch steht Ihnen eine Anerkennung von
          einer Versuchspersonenstunde zu, wenn das Experiment aus technischen
          oder anderen nicht in Ihrer Macht liegenden Gründen nicht beendet
          werden kann. Nehmen Sie in diesem Fall Kontakt mit der Versuchsleitung
          auf. Eine finanzielle Aufwandsentschädigung ist für dieses Experiment
          nicht vorgesehen.
        </p>
        <br />
        <!-- The $magpie field gives you access to magpie-specific functionality -->
        <button @click="$magpie.nextScreen">Weiter</button>
      </Screen>

      <Screen
        :title="'Hinweise zur Durchführung dieses Versuchs'"
        class="instructions"
      >
        <strong>Vorschlag von MF:</strong>
        <p>Schalten sie das Experiment auf Fullscreen (wie macht man das?).</p>
        <p>Benutzen Sie eine Maus.</p>
        <p>
          Schaffen Sie sich Platz für die Mausbewegung. Sie sollten den
          Mauszeiger in einer Bewegung ohne Abheben der Maus von der unteren zur
          oberen Bildschirmkannte bewegen können.
        </p>
        <p>
          Wenn Sie können, wären wir Ihnen dankbar, wenn Sie die Geschwindigkeit
          der Maus in Ihren Systemeinstellungen verlangsamen könnten, so dass es
          Ihnen gerade noch mühelos gelingt, in einer Armbewegung den Mauszeiger
          von der unteren zur oberen Bildschirmkante zu bewegen.
        </p>
        <br />
        <!-- The $magpie field gives you access to magpie-specific functionality -->
        <button @click="$magpie.nextScreen">Weiter</button>
      </Screen>

      <Screen :title="'Instruktionen'" class="instructions">
        <p>
          Bitte lesen Sie diese Instruktionen aufmerksam durch und versuchen
          Sie, diese während des Experimentverlaufs so nah wie möglich zu
          befolgen.
        </p>
        <h3>Ablauf</h3>
        <p>
          Bitte bewegen Sie zu Beginn eines jeden Durchgangs den Mauszeiger zum
          Startpunkt. Dies ist der blaue Knopf mit dem Label "GO" am unteren
          Bildschirmrand. Sie starten jeden Durchgang selbst, indem Sie den
          Startknopf anklicken. Pro Durchgang wird Ihnen ein kurzer Satz Wort
          für Wort angezeigt. Am oberen Bildschirmrand sehen Sie zwei
          Antwortflächen, je eine für »wahr« (w) und eine für »falsch« (f).
          Bitte klicken Sie zügig auf die richtige Antwortfläche, je nachdem, ob
          Sie einen wahren oder einen falschen Satz gelesen haben.
        </p>
        <p>
          Bitte beginnen Sie unmittelbar mit Erscheinen des letzten Wortes des
          Satzes, den Mauszeiger in Richtung der Antwortflächen am oberen
          Bildschirmrand zu bewegen. Sollten Sie den Mauszeiger am Satzende
          nicht schnell genug nach oben bewegen, erscheint auf dem Bildschirm
          ein Warnsignal, nämlich ein “!!!”. Das ist nicht weiter schlimm. Es
          soll Sie nur daran erinnern, beim nächsten Durchgang die Maus zügiger
          bei Erscheinen des letzten Wortes nach oben zu bewegen.
        </p>
        <p>
          Nachdem Sie Ihre Wahl getroffen haben, verschwinden die beiden
          Antwortflächen und der Startknopf. Bitte nutzen Sie diese
          »Verschnaufspause«, um den Mauszeiger wieder in die Startregion
          zurückzuführen. Sobald der Startknopf wieder erscheint, können Sie in
          Ruhe den nächsten Durchgang starten, indem Sie erneut den Startpunkt
          anklicken.
        </p>
        <p>
          Auch wenn das Experiment nur etwa 20 Minuten dauern wird, kann die
          Ihnen gestellte Aufgabe eintönig werden, so dass Sie vielleicht bald
          das Gefühl haben könnten, mit Ihren Reaktionen »in einen Trott« zu
          geraten. Bitte achten Sie darauf, Ihre Konzentration auf die Aufgabe
          über den gesamten Verlauf des Experiments aufrechtzuerhalten! Nutzen
          Sie gerne die Phasen vor einem Klick auf den Startpunkt, um
          beispielsweise Ihren Arm neu zu positionieren oder einfach kurz
          durchzuatmen.
        </p>
        <h3>Auf einen Blick:</h3>
        <ul>
          <li>
            Beginnen Sie die Mausbewegung unmittelbar mit Erscheinen des letzten
            Wortes des Satzes.
          </li>
          <li>
            Antworten Sie zügig. Bei Verzögerungen erinnert Sie ein
            eingeblendetes “!!!” daran, beim nächsten Durchgang etwas schneller
            zu sein.
          </li>
          <li>
            Achten Sie aufmerksam und konzentriert auf die Sätze, die Ihnen
            präsentiert werden und versuchen Sie, stets die richtige Antwort
            anzuklicken.
          </li>
          <li>
            Nutzen Sie gerne die Pausen zwischen einzelnen Durchgängen zum
            Verschnaufen, damit Sie konzentriert und doch angenehm arbeiten
            können.
          </li>
        </ul>
        <p>Viel Spaß beim Experiment und vielen Dank für Ihre Teilnahme!</p>
        <button @click="$magpie.nextScreen">Trainingsphase starten</button>
      </Screen>

      <!-- Measure mouse speed -->
      <Screen>
        <template #0="{ responses }">
          <CategorizationMousetracking :select-event="'mouseover'">
            <template #option1>
              <div class="optionBox">
                w
              </div>
            </template>
            <template #option2>
              <div class="optionBox">
                f
              </div>
            </template>
            <template #stimulus>
              <Timer key="mouse-time" v-model="responses.timer" />
            </template>
            <template #feedback>
              <Wait
                :time="0"
                @done="
                  mouse_speed_time = responses.timer();
                  $magpie.nextScreen();
                "
              />
            </template>
          </CategorizationMousetracking>
        </template>
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

export default {
  name: 'App',
  components: { TrialScreen },
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
      training_length: training.length,
      mouse_speed_time: 0
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
    }
  }
};
</script>
<style>
.instructions {
  text-align: left;
}
</style>
