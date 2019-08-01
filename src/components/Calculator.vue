<template>
    <div>
        <div class="form-inline d-flex mb-2">
            <div class="form-group mr-4">
                <label for="sum">Target Sum</label>
                <input type="number"
                       class="form-control"
                       v-model.number="target"
                       id="sum"
                />
            </div>
            <div class="form-group">
                <label for="setArray">Set Array from String</label>
                <input type="text"
                       class="form-control"
                       v-model="newArray"
                       id="setArray"
                >
            </div>
            <button class="add-btn btn btn-primary btn-md"
                    @click.prevent="setFromString"
            >
                SET
            </button>
        </div>
        <number-list :set="set" />
        <div class="d-flex justify-content-end mt-4 align-content-center">
            <button class="btn btn-outline-danger btn-lg mr-2"
                    @click.prevent="reset"
            >
                Reset
            </button>

            <button class="btn btn-success btn-lg"
                :class="{ 'disabled': set.length < 2 }"
                :disabled="set.length < 2"
                @click.prevent="calculate"
            >
                Calculate!
            </button>
        </div>

        <div class="card my-3" v-if="result.length > 0">
            <div class="card-body">
                <h5 class="card-title">
                    Results ({{ result.length + ' generated in ' + calcTime + 'ms' }})
                </h5>
                <ul class="p-0">
                    <li v-for="(r, index) in result"
                        class="d-flex justify-content-between bg-light p-2 pr-3 ml-0"
                        :key="'result_' + index"
                    >
                        {{ r }}
                    </li>
                </ul>
            </div>
        </div>

        <div v-if="calculations > 1 && result.length === 0"
            class="alert alert-warning mt-4"
        >
            Set returned no results!
        </div>
    </div>
</template>

<script>
import NumberList from './NumberList.vue';

export default {
  name: 'calculator',
  components: { NumberList },
  data() {
    return {
      set: [2, 4, 6, 8, 10, 12, 14, 16, 18],
      target: 30,
      newArray: '',
      result: [],
      calculations: 0,
      calcTime: 0
    };
  },

  methods: {
    calculate() {
      this.reset();
      this.findSubsetSums(this.set, this.target);
    },
    reset() {
      this.result = [];
      this.calculations = 0;
      this.calcTime = 0;
    },
    setFromString() {
      this.set = JSON.parse('[' + this.newArray + ']');
      this.newArray = '';
    },
    findSubsetSums(set, target, partial) {
      let start = performance.now();

      this.calculations += 1;

      let sum;
      let num;
      let remaining;
      const nums = this.dedupeArray(set);

      partial = partial || [];
      sum = this.sumArray(partial);

      if (sum > target) return null;

      if (sum === target && partial.length > 1) {
        this.result.push(partial);
      }

      for (let i = 0; i < nums.length; i += 1) {
        num = nums[i];
        remaining = nums.slice(i + 1);
        this.findSubsetSums(remaining, target, partial.concat([num]));
      }

      let finish = performance.now();
      this.calcTime = finish - start;
      return this.result;
    },
    dedupeArray(arr) {
      return arr.filter((n, i) => arr.indexOf(n) === i);
    },
    sumArray(arr) {
      return arr.reduce((a, b) => a + b, 0);
    },
  },
};
</script>

<style>
    label {
        font-weight: 700;
    }
</style>
