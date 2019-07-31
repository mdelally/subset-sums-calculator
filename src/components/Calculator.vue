<template>
    <div>

        <div class="form-group">
            <label for="sum">Target Sum</label>
            <input type="number"
                   class="form-control"
                   v-model.number="sum"
                   id="sum"
            >
        </div>

        <div class="card">
            <div class="card-body">
                <h5 class="card-title">Set to Calculate</h5>
                <ul>
                    <li v-for="(n, index) in set"
                        class="d-flex justify-content-between"
                    >
                        <span>{{ n }}</span>
                        <button class="btn btn-danger btn-sm"
                                @click.prevent="deleteNumFromSet(index)"
                        >
                            DELETE
                        </button>
                    </li>
                </ul>

                <div class="form-inline d-flex justify-content-end">
                    <div class="form-group">
                        <label for="addToSet">Add to Set</label>
                        <input type="number"
                               class="form-control"
                               v-model.number="newNum"
                               id="addToSet"
                        >
                    </div>
                    <button class="add-btn btn btn-primary btn-md"
                            @click.prevent="addNumToSet"
                    >
                        ADD
                    </button>
                </div>
            </div>
        </div>

        <div class="d-flex justify-content-end m-4">
            <button class="btn btn-success btn-lg">
                Calculate!
            </button>
        </div>
    </div>
</template>

<script>
  export default {
    name: 'calculator',
    data() {
      return {
        set: [5,15,1,3,8,7,15],
        sum: 30,
        newNum: 1
      }
    },

    computed: {
      results() {

      }
    },

    methods: {
      addNumToSet() {
        this.set.push(newNum);
        this.newNum = 1;
      },
      deleteNumFromSet(index) {
        this.set.splice(index, 1);
      }
    }
  }
</script>

<style scoped>
    label {
        font-weight: 700;
    }

    div.form-inline > div.form-group label {
        margin-right: 6px;
    }

    button.add-btn {
        margin-left: 6px;
    }

    li {
        margin-bottom: 8px;
        background-color: #e6e6e6;
        padding: 2px 6px;
        border-radius: 3px;
    }

    li > span {
        font-weight: 700;
    }
</style>
