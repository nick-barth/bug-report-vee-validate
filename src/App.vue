<template>
  <div>
    <div @click="isThingOpen = !isThingOpen">Toggle is open</div>
    <div v-if="isThingOpen">
      <Form
        @submit="onSubmit"
        :validation-schema="schema"
        :initialValues="initialValues"
      >
        <Field name="email" type="email" />
        <ErrorMessage name="email" />

        <Field name="password" type="password" />
        <ErrorMessage name="password" />

        <button>Submit</button>
      </Form>
    </div>
  </div>
</template>

<script>
import { Form, Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";

export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  data() {
    const schema = yup.object({
      email: yup.string().required().email(),
      password: yup.string().required().min(8),
    });

    const initialValues = {
      email: "wow",
      password: "no",
    };

    return {
      isThingOpen: false,
      schema,
      initialValues,
    };
  },
  methods: {
    onSubmit(values) {
      // Submit values to API...
      alert(JSON.stringify(values, null, 2));
    },
  },
};
</script>
