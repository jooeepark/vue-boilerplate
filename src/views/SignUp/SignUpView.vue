<template>
  <div class="sign-up container">
    <h1>This is an about page</h1>

    <Form class="sign-up__form">
      <component
        :is="stages[nowStage].stage"
        @update:stage="updateStage"
      ></component>
    </Form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import Form from "@/components/Form/index.vue";
import FormInnerIntro from "./FormInnerIntro.vue";
import FormInnerID from "./FormInnerID.vue";
import FormInnerPassword from "./FormInnerPassword.vue";
import FormInnerBirthday from "./FormInnerBirthday.vue";
import FormInnerEmail from "./FormInnerEmail.vue";
import FormInnerFinish from "./FormInnerFinish.vue";

export default defineComponent({
  name: "HomeView",
  components: {
    Form,
    FormInnerIntro,
    FormInnerID,
    FormInnerPassword,
    FormInnerBirthday,
    FormInnerEmail,
    FormInnerFinish,
  },
  setup() {
    const nowStage = ref(0);
    const stages = ref([
      { stage: "FormInnerIntro", checked: true },
      { stage: "FormInnerID", checked: false },
      { stage: "FormInnerPassword", checked: false },
      { stage: "FormInnerBirthday", checked: false },
      { stage: "FormInnerEmail", checked: false },
      { stage: "FormInnerFinish", checked: false },
    ]);

    const updateStage = (payload: { stage: string; checked: boolean }) => {
      stages.value = stages.value.map((stage) =>
        stage.stage === payload.stage ? payload : stage
      );

      let flag = false;
      let stageCount = 0;

      stages.value.forEach((stage, index) => {
        if (flag) return;
        if (stage.checked) {
          flag = true;
        }
        stageCount = index;
      });

      nowStage.value = stageCount;
    };

    return {
      nowStage,
      stages,
      updateStage,
    };
  },
});
</script>

<style lang="scss" scoped>
:global(.form-inner) {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.sign-up {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .sign-up__form {
    overflow: hidden;
    display: flex;
    flex-direction: column;

    position: relative;

    min-height: 400px;

    .stage-enter-active {
      position: relative;
      transition: all 0.5s ease-in-out;
    }

    .stage-enter-from {
      opacity: 0;
      transform: translate3d(200px, 0px, 0px);
    }

    .stage-enter-to {
      opacity: 1;
    }

    .stage-leave-active {
      transition: all 0.25s ease-in-out;
    }

    .stage-leave-to {
      transform: translate3d(-200px, 0px, 0px);
      opacity: 0;
    }
  }
}
</style>
