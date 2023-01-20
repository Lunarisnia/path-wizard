<template>
    <v-container class="fill-height">
        <v-responsive class="d-flex align-center fill-height">
            <v-row align='center' no-gutters style="height: 150px;" v-for="i in row" :key="i">
                <v-col v-for="j in col" :key="j" class="child-flex">
                    <v-img class="mx-auto"
                        src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f2/Playing_card_spade_2.svg/800px-Playing_card_spade_2.svg.png"
                        width="100" />
                </v-col>
            </v-row>
        </v-responsive>
    </v-container>
</template>

<script lang="ts">
interface Card {
    class: string,
    item: string,
    legalMove: Array<Array<Number>>,
    removed: boolean,
}
export default {
    props: {
        col: Number,
        row: Number,
    },
    setup(props) {
        props.col // type: number | undefined
        props.row // type: number | undefined
    },
    mounted() {
        this.grid = [
            [{} as Card, {} as Card,]
        ];
    },
    data() {
        return {
            grid: [] as Array<Array<Card>>
        };
    }
}
</script>