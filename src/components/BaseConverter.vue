<template>
  <div class="BaseConverter box">
    <template v-if="isLoading">
      <b-loading v-model="isLoading"></b-loading>
    </template>
    <template v-else>
      <div class="BaseConverter__inputs">
        <b-field
          label="Enter a number"
          :type="!isValid ? 'is-danger' : undefined"
          :message="!isValid ? 'Invalid number' : undefined"
          @input.native="!isValid ? resetValidation : undefined"
        >
          <b-input v-model="inputValue"></b-input>
        </b-field>
        <div class="columns">
          <div class="column">
            <b-field label="From Base">
              <b-select v-model="sourceBase" expanded>
                <option
                  v-for="option in baseValues"
                  :value="option.value"
                  :key="option.value"
                >
                  {{ option.text }}
                </option>
              </b-select>
            </b-field>
          </div>
          <div class="column">
            <b-field label="Target Base">
              <b-select v-model="targetBase" expanded>
                <option
                  v-for="option in baseValues"
                  :value="option.value"
                  :key="option.value"
                >
                  {{ option.text }}
                </option>
              </b-select>
            </b-field>
          </div>
        </div>
        <b-button
          type="is-primary"
          expanded
          @click="onSubmit"
          :disabled="isDisabled"
          >Convert</b-button
        >
      </div>
      <div class="BaseConverter__results">
        <b-field label="Result">
          <b-input type="textarea" v-model="outputValue" expanded />
        </b-field>
      </div>
    </template>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { SelectOption } from "@/types/component";

@Component({})
export default class BaseConverter extends Vue {
  isLoading = true;
  isValid = true;

  inputValue = "";
  outputValue = "";
  sourceBase = 0;
  targetBase = 0;

  mounted() {
    this.isLoading = false;
  }

  get isDisabled() {
    return !this.inputValue.length || !this.sourceBase || !this.targetBase;
  }

  get baseValues() {
    const bases: Array<SelectOption> = [];

    for (let i = 1; i <= 32; i++) {
      bases.push({ text: i.toString(), value: i });
    }

    return bases;
  }

  onSubmit() {
    console.log("onSubmit");
    // Return result or return error message
    const result = this.convertNumber(
      this.inputValue,
      this.sourceBase,
      this.targetBase
    );

    if (!result) {
      this.outputValue = "No result";
    } else {
      this.outputValue = result;
    }
  }

  convertNumber(input: string, sourceBase: number, targetBase: number) {
    const _input = parseInt(input);
    if (!_input) {
      this.isValid = false;
      return undefined;
    }

    return parseInt(input, sourceBase).toString(targetBase);
  }
}
</script>

<style scoped lang="scss">
.BaseConverter {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 30rem;
  width: 20rem;
}

.BaseConverter__inputs {
  width: 100%;
}

.BaseConverter__results {
  margin-top: 2rem;
  width: 100%;
}
</style>
