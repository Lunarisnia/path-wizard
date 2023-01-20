<template>
    <v-container class="fill-height">
        <v-btn @click="separateVisualization()">Separate Visualization</v-btn>
        <v-btn @click="resetAllCard()">Reset All Card</v-btn>
        <v-btn @click="closeHalfCard()">Close Half Card</v-btn>
        <v-btn @click="openAllCard()">Open All Card</v-btn>
        <!-- <v-btn @click="openHalfCard('A')">Open 1</v-btn>
        <v-btn @click="openHalfCard('B')">Open 2</v-btn> -->
        <v-responsive class="d-flex align-center fill-height">
            <v-row align='center' no-gutters style="height: 150px;" v-for="i in row" :key="i">
                <v-col v-for="j in col" :key="j" class="child-flex">
                    <v-img class="mx-auto" :src='grid[i-1][j-1].status ? grid[i-1][j-1].item : removedCard' width="100" @click="removeACard(i - 1, j - 1)" />
                    <!-- <v-btn @click="removeACard(i - 1, j - 1)">{{ i- 1 }}, {{ j- 1 }}</v-btn> -->
                </v-col>
            </v-row>
        </v-responsive>
    </v-container>
</template>

<script lang="ts">
interface Card {
    class: string,
    status: number,
    item?: string,
}
const defaultCardSetA: string = "https://deckofcardsapi.com/static/img/KS.png";
const defaultCardSetB: string = "https://upload.wikimedia.org/wikipedia/commons/thumb/5/57/Playing_card_heart_A.svg/819px-Playing_card_heart_A.svg.png";
const cardImageList: Array<string> = [
    "https://deckofcardsapi.com/static/img/AH.png",
    "https://deckofcardsapi.com/static/img/2H.png",
    "https://deckofcardsapi.com/static/img/3H.png",
    "https://deckofcardsapi.com/static/img/4H.png",
    "https://deckofcardsapi.com/static/img/5H.png",
    "https://deckofcardsapi.com/static/img/6H.png",
    "https://deckofcardsapi.com/static/img/7H.png",
    "https://deckofcardsapi.com/static/img/8H.png",
    "https://deckofcardsapi.com/static/img/9H.png",
    "https://deckofcardsapi.com/static/img/0H.png",
    "https://deckofcardsapi.com/static/img/JH.png",
    "https://deckofcardsapi.com/static/img/QH.png",
    "https://deckofcardsapi.com/static/img/KH.png",

    "https://deckofcardsapi.com/static/img/AD.png",
    "https://deckofcardsapi.com/static/img/2D.png",
    "https://deckofcardsapi.com/static/img/3D.png",
    "https://deckofcardsapi.com/static/img/4D.png",
    "https://deckofcardsapi.com/static/img/5D.png",
    "https://deckofcardsapi.com/static/img/6D.png",
    "https://deckofcardsapi.com/static/img/7D.png",
    "https://deckofcardsapi.com/static/img/8D.png",
    "https://deckofcardsapi.com/static/img/9D.png",
    "https://deckofcardsapi.com/static/img/0D.png",
    "https://deckofcardsapi.com/static/img/JD.png",
    "https://deckofcardsapi.com/static/img/QD.png",
    "https://deckofcardsapi.com/static/img/KD.png",

    "https://deckofcardsapi.com/static/img/AS.png",
    "https://deckofcardsapi.com/static/img/2S.png",
    "https://deckofcardsapi.com/static/img/3S.png",
    "https://deckofcardsapi.com/static/img/4S.png",
    "https://deckofcardsapi.com/static/img/5S.png",
    "https://deckofcardsapi.com/static/img/6S.png",
    "https://deckofcardsapi.com/static/img/7S.png",
    "https://deckofcardsapi.com/static/img/8S.png",
    "https://deckofcardsapi.com/static/img/9S.png",
    "https://deckofcardsapi.com/static/img/0S.png",
    "https://deckofcardsapi.com/static/img/JS.png",
    "https://deckofcardsapi.com/static/img/QS.png",
    "https://deckofcardsapi.com/static/img/KS.png",

    "https://deckofcardsapi.com/static/img/AC.png",
    "https://deckofcardsapi.com/static/img/2C.png",
    "https://deckofcardsapi.com/static/img/3C.png",
    "https://deckofcardsapi.com/static/img/4C.png",
    "https://deckofcardsapi.com/static/img/5C.png",
    "https://deckofcardsapi.com/static/img/6C.png",
    "https://deckofcardsapi.com/static/img/7C.png",
    "https://deckofcardsapi.com/static/img/8C.png",
    "https://deckofcardsapi.com/static/img/9C.png",
    "https://deckofcardsapi.com/static/img/0C.png",
    "https://deckofcardsapi.com/static/img/JC.png",
    "https://deckofcardsapi.com/static/img/QC.png",
    "https://deckofcardsapi.com/static/img/KC.png",
];
const shuffleArray = (array: Array<any>) => {
    let currentIndex = array.length,  randomIndex;

    // While there remain elements to shuffle.
    while (currentIndex != 0) {

        // Pick a remaining element.
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;

        // And swap it with the current element.
        [array[currentIndex], array[randomIndex]] = [
        array[randomIndex], array[currentIndex]];
    }

    return array;
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
    data() {
        return {
            grid: [
                [{ class: "A", item: defaultCardSetA, status: 1 }, { class: "B", item: defaultCardSetB, status: 1 }, { class: "A", item: defaultCardSetA, status: 1 }, { class: "B", item: defaultCardSetB, status: 1 }, { class: "A", item: defaultCardSetA, status: 1 }],
                [{ class: "B", item: defaultCardSetB, status: 1 }, { class: "A", item: defaultCardSetA, status: 1 }, { class: "B", item: defaultCardSetB, status: 1 }, { class: "A", item: defaultCardSetA, status: 1 }, { class: "B", item: defaultCardSetB, status: 1 }],
                [{ class: "A", item: defaultCardSetA, status: 1 }, { class: "B", item: defaultCardSetB, status: 1 }, { class: "A", item: defaultCardSetA, status: 1 }, { class: "B", item: defaultCardSetB, status: 1 }, { class: "A", item: defaultCardSetA, status: 1 }],
                [{ class: "B", item: defaultCardSetB, status: 1 }, { class: "A", item: defaultCardSetA, status: 1 }, { class: "B", item: defaultCardSetB, status: 1 }, { class: "A", item: defaultCardSetA, status: 1 }, { class: "B", item: defaultCardSetB, status: 1 }]
            ] as Array<Array<Card>>,
            removedCard: "https://cutewallpaper.org/24/playing-card-back-png/colorful-38b1d-poker-3f9cb-card-65195-back-f3490-opengameartorg.png",
        };
    },
    methods: {
        removeACard(row: number, col: number) {
            this.grid[row][col].status = 0;
        },
        separateVisualization() {
            this.grid = this.grid.map((row: Array<Card>) => {
                return row.map((col: Card) => ({ ...col, item: col.class === 'A' ? defaultCardSetA : defaultCardSetB }))
            })
        },
        resetAllCard() {
            const cil : Array<string> = shuffleArray(cardImageList.concat());
            this.grid = this.grid.map((row: Array<Card>) => {
                return row.map((col: Card) => ({ ...col, item: cil.pop() }))
            });
        },
        closeAllCard() {
            this.grid = this.grid.map((row: Array<Card>) => {
                return row.map((col: Card) => ({ ...col, status: 0 }))
            });
        },
        closeHalfCard() {
            const targetClass: string = ["A", "B"][Math.floor(Math.random() * 2)];
            this.grid = this.grid.map((row: Array<Card>) => {
                return row.map((col: Card) => col.class === targetClass ? col : ({ ...col, status: 0 }));
            });
        },
        openAllCard() {
            this.grid = this.grid.map((row: Array<Card>) => {
                return row.map((col: Card) => col.status ? col : ({ ...col, status: 1 }));
            });
        }
    }
}
</script>