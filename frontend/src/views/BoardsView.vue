<template>
  <div class="boards mt-3">
    <div class="col-12 row px-5" :list="boards" group="boards">
      <div
        class="col-lg-2 col-md-4 col-sm-6 col-12 my-2"
        v-for="(board, boardindex) in boards"
        :key="board.id"
        :index="boardindex">
        <b-card
        overlay
        footer="Card Footer"
        footer-tag="footer"
        :img-src="board.background"
        img-alt="Card Image"
        text-variant="white"
        :title="board.name"
        class=""
      >
        <b-card-text>
        </b-card-text>
        </b-card>
        <b-icon icon="file-earmark-excel-fill" class="remove-board" v-on:click="removeBoard(board._id)"></b-icon>
      </div>
      <div class="col-lg-2 col-md-4 col-sm-6 col-12 my-2">
        <a>add card</a>
      </div>
    </div>

  </div>
</template>
<script>
import axios from 'axios';

export default {
  name: 'BoardsView',
  data() {
    return {
      boards: '',
    };
  },
  created() {
    // Board list get
    axios.get('http://localhost:3030/boards').then((res) => {
      console.log('res-------->', res.data.data);
      this.boards = res.data.data;
    });
  },
  methods: {
    removeBoard(id) {
      axios.delete(`http://localhost:3030/boards/${id}`).then((res) => {
        console.log(res.data);
        const index = this.boards.map((data) => data.id).indexOf(id);
        this.boards.splice(index, 1);
      });
    },
  },
};
</script>

<style scoped>
  footer {
    background-color: #fff;
    color: #000;
  }
  .card {
    box-shadow: 0 3px 1px -2px rgba(0,0,0,.2),0 2px 2px 0 rgba(0,0,0,.14),0 1px 5px 0 rgba(0,0,0,.12)!important;
    cursor: pointer;
  }

  .remove-board {
    position: relative;
    margin-top: -28px;
    right: 20px;
    float: right;
    cursor: pointer;
  }

  .remove-card:hover {
    transform: scale(1.5);
  }
</style>
