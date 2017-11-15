<template>
  <div class="container">
    <div class="stepWrapper" v-if="active !== 'summary'">
      <Steps
        v-for="step in steps"
        :key="step.id"
        :step="step"
        @goToStep="goToStep"
      >
      </Steps>
    </div>
    <StepOne
      v-if="active === 1"
      @getNext="getSecond"
    >
    </StepOne>
    <StepTwo
      v-else-if="active === 2"
      @getNext="getThird"
      @getPrev="getPrev"
    >
    </StepTwo>
    <StepThree
      v-else-if="active === 3"
      @getNext="getForth"
      @getPrev="getPrev"
    >
    </StepThree>
    <StepFour
      v-else-if="active === 4"
      @getNext="getSummary"
      @getPrev="getPrev"
    ></StepFour>
    <TheEnd
      v-else-if="active === 'summary'"
      :user="user"
      @getNext="andAgain"
    >
    </TheEnd>
  </div>
</template>

<script>
  import Steps from './components/Steps.vue'
  import StepOne from './components/steps/StepOne.vue'
  import StepTwo from './components/steps/StepTwo.vue'
  import StepThree from './components/steps/StepThree.vue'
  import StepFour from './components/steps/StepFour.vue'
  import TheEnd from './components/TheEnd.vue'

  export default {
    components: {
      Steps, StepOne, StepTwo, StepThree, StepFour, TheEnd
    },
    data() {
      return {
        user: {},
        active: 1,
        steps: [
          {id: 1, style: 'step active'},
          {id: 2, style: 'step'},
          {id: 3, style: 'step'},
          {id: 4, style: 'step'}
        ]
      }
    },
    methods: {
      goToStep(stepId) {
        this.steps.forEach(step => {
          if (stepId === step.id) {
            if (step.style === 'step passed' || step.style === 'step active') {
              this.active = stepId;
            }
          }
        });
      },
      getPrev() {
        this.active = this.active - 1;
      },
      getSecond(data) {
        this.steps.forEach(step => {
          if (step.id === 1) {
            step.style = 'step passed';
          } else if (step.id === 2 && step.style === 'step') {
            step.style = 'step active';
          }
        });
        this.active = 2;
        for (let key in data) {
          if (data.hasOwnProperty(key)) {
            this.user[key] = data[key];
          }
        }
      },
      getThird(data) {
        this.steps.forEach(step => {
          if (step.id === 2) {
            step.style = 'step passed';
          } else if (step.id === 3 && step.style === 'step') {
            step.style = 'step active';
          }
        });
        this.active = 3;
        for (let key in data) {
          if (data.hasOwnProperty(key)) {
            this.user[key] = data[key];
          }
        }
      },
      getForth(data) {
        this.steps.forEach(step => {
          if (step.id === 3) {
            step.style = 'step passed';
          } else if (step.id === 4 && step.style === 'step') {
            step.style = 'step active';
          }
        });
        this.active = 4;
        for (let key in data) {
          if (data.hasOwnProperty(key)) {
            this.user[key] = data[key];
          }
        }
      },
      getSummary(data) {
        this.active = 'summary';
        for (let key in data) {
          if (data.hasOwnProperty(key)) {
            this.user[key] = data[key];
          }
        }
      },
      andAgain() {
        this.user = {};
        this.active = 1;
        this.steps.forEach(step => {
          if (step.id === 1) {
            step.style = 'step active';
          } else {
            step.style = 'step';
          }
        });
      }
    }
  }
</script>

<style scoped>
  .container {
    margin: 10% 0 0 29%;;
    animation-name: fadeIn;
    animation-duration: 1s;
  }

  .stepWrapper {
    display: inline-flex;
  }

</style>
