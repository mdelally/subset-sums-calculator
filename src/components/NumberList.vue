<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">
                Set to Calculate ({{ set.length }} values)
            </h5>

            <div v-if="set.length < 2" class="alert alert-danger">
                <em class="p-1 font-weight-bold">Set must contain 2 or more values!</em>
            </div>

            <div class="form-inline d-flex justify-content-end mb-2">
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
                <button class="add-btn btn btn-danger btn-md"
                        @click.prevent="set = []"
                >
                    DELETE ALL
                </button>
            </div>
            <ul class="number-list p-0" id="list">
                <li v-for="(n, index) in set"
                    class="d-flex justify-content-between bg-light p-2 pr-3"
                    :key="'num_' + index"
                >
                    <span>{{ n }}</span>
                    <button class="btn btn-danger btn-sm"
                            @click.prevent="deleteNumFromSet(index)"
                    >
                        DELETE
                    </button>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
  name: 'number-list',

  props: ['set'],

  data() {
    return {
      newNum: 1,
    };
  },

  methods: {
    addNumToSet() {
      this.set.push(this.newNum);
      this.newNum = 1;

      let list = document.getElementById("list");
      this.$nextTick(() => {
        list.scrollTop = list.scrollHeight;
      });
    },
    deleteNumFromSet(index) {
      this.set.splice(index, 1);
    },
  },
};
</script>

<style>
    ul.number-list {
        max-height: 300px;
        overflow: scroll;
    }

    div.form-inline > div.form-group label {
        margin-right: 6px;
    }

    button.add-btn {
        margin-left: 6px;
    }

    li {
        margin-bottom: 8px;
        /*background-color: #e6e6e6;*/
        /*padding: 2px 6px;*/
        border-radius: 3px;
    }

    li > span {
        font-weight: 700;
    }
</style>
