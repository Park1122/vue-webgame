<template>
    <td @click="onClickTd">{{cellData}}</td>
</template>
<script>
    export default {
        props: {
            cellData: String,
            rowIndex: Number,
            cellIndex: Number
        },
        methods: {
            onClickTd() {
                if(this.cellData) return;

                let rootData = this.$root.$data;
                this.$set(rootData.tableData[this.rowIndex], this.cellIndex, rootData.turn);

                let win = false;
                //3목 체크 로직
                if (rootData.tableData[this.rowIndex][0] === rootData.turn && rootData.tableData[this.rowIndex][1] === rootData.turn && rootData.tableData[this.rowIndex][2] === rootData.turn) {
                    win = true;
                }
                if (rootData.tableData[0][this.cellIndex] === rootData.turn && rootData.tableData[1][this.cellIndex] === rootData.turn && rootData.tableData[2][this.cellIndex] === rootData.turn) {
                    win = true;
                }
                if (rootData.tableData[0][0] === rootData.turn && rootData.tableData[1][1] === rootData.turn && rootData.tableData[2][2] === rootData.turn) {
                    win = true;
                }
                if (rootData.tableData[0][2] === rootData.turn && rootData.tableData[1][1] === rootData.turn && rootData.tableData[2][0] === rootData.turn) {
                    win = true;
                }

                if(win) {
                    rootData.winner = rootData.turn;
                    rootData.turn = 'O';
                    rootData.tableData = [['', '', ''], ['', '', ''], ['', '', '']];
                } else {
                    let all = true; // 무승부 여부
                    //무승부 체크
                    rootData.tableData.forEach((row) => {
                        row.forEach((cell) => {
                            if(!cell) {
                                all = false;
                            }
                        });
                    });

                    if(all) { //무승부인 경우
                        rootData.turn = 'O';
                        rootData.winner = '';
                        rootData.tableData = [['', '', ''], ['', '', ''], ['', '', '']];
                    }
                    rootData.turn = rootData.turn === 'O' ? 'X' : 'O';
                }
            }
        }
    }
</script>