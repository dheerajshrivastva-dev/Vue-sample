<template>
  <div class="container">
    <button @click="handleClose" class="close-button">X</button>
  <form @submit.prevent="handleSubmit">
    <div class="input-container">
    <label for="name">Name:</label>
    <input v-model="name" id="name" required>
  </div>
    <br>
    <div class="input-container">
    <label for="age">Age:</label>
    <input v-model.number="age" id="age" type="number" required>
  </div>
    <br>
    <div class="input-container">
    <label for="email">Email:</label>
    <input v-model="email" id="email" type="email" required>
  </div>
    <br>

    <button type="submit" id="submit">Create Data</button>
  </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, type PropType } from 'vue';

interface FormProps {
  onSubmit: (name: string, age: number, email: string) => void;
  onClose?: () => void;
}

export default defineComponent({
  name: 'DataForm',
  props: {
    onSubmit: {
      type: Function as PropType<FormProps['onSubmit']>,
      required: true,
    },
    onClose: {
      type: Function as PropType<FormProps['onClose']>,
      required: false,
    }
  },
  setup(props: FormProps) {
    const name = ref('');
    const age = ref(0);
    const email = ref('');

    const handleSubmit = () => {
      props.onSubmit(name.value, age.value, email.value);
    };

    const handleClose = () => {
      props?.onClose?.();
    }

    return {
      name,
      age,
      email,
      handleSubmit,
      handleClose,
    };
  },
});
</script>

<style scoped>

.container {
  display: flex;
  position: relative;
}

form {
  display: flex;
  flex-direction: column;
  gap:8px;;
}
.input-container {
  display: flex;
  gap: 20px;
}

.input-container label {
  width: 40px;
}

#submit {
  padding: 8px 16px;
  flex-grow: 1;
  color: antiquewhite;
  background-color: rgb(42, 99, 42);
  border: none;
  outline: whitesmoke;
  border-radius: 4px;
}

.close-button {
  background-color: #fff5;
  border: none;
  color: #ffa;
  border-radius: 15px;
  width: 30px;
  height: 30px;
  position: absolute;
  top: -30px;
  right: -30px;
  z-index: 10001;
}
</style>
