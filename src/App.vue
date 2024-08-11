<script setup>
import { ref } from "vue";
import {
    allianceCombinations,
    hordeCombinations,
    specs,
} from "./components/info";

var factionChoice = ref("Doesn't matter");
var faction = ref("");
var race = ref("");
var cclass = ref("");
var spec = ref("");

function generate() {
    var randomClass;
    var randomSpec;
    var randomRace;
    var coinFlip = () => Math.random() >= 0.5;
    var randomFaction = coinFlip() ? "Alliance" : "Horde";
    switch (factionChoice.value) {
        case "Alliance":
            randomClass =
                Object.keys(allianceCombinations)[
                    Math.floor(
                        Math.random() * Object.keys(allianceCombinations).length
                    )
                ];
            randomSpec =
                specs[randomClass][
                    Math.floor(Math.random() * specs[randomClass].length)
                ];
            randomRace =
                allianceCombinations[randomClass][
                    Math.floor(
                        Math.random() * allianceCombinations[randomClass].length
                    )
                ];
            break;
        case "Horde":
            randomClass =
                Object.keys(hordeCombinations)[
                    Math.floor(
                        Math.random() * Object.keys(hordeCombinations).length
                    )
                ];
            randomSpec =
                specs[randomClass][
                    Math.floor(Math.random() * specs[randomClass].length)
                ];
            randomRace =
                hordeCombinations[randomClass][
                    Math.floor(
                        Math.random() * hordeCombinations[randomClass].length
                    )
                ];
            break;
        default:
            randomClass = Object.keys(
                randomFaction === "Alliance"
                    ? allianceCombinations
                    : hordeCombinations
            )[
                Math.floor(
                    Math.random() *
                        Object.keys(
                            randomFaction === "Alliance"
                                ? allianceCombinations
                                : hordeCombinations
                        ).length
                )
            ];
            randomSpec =
                specs[randomClass][
                    Math.floor(Math.random() * specs[randomClass].length)
                ];
            randomRace = (
                randomFaction === "Alliance"
                    ? allianceCombinations
                    : hordeCombinations
            )[randomClass][
                Math.floor(
                    Math.random() *
                        (randomFaction === "Alliance"
                            ? allianceCombinations
                            : hordeCombinations)[randomClass].length
                )
            ];
            break;
    }
    cclass.value = randomClass.charAt(0).toUpperCase() + randomClass.slice(1);
    race.value = randomRace.charAt(0).toUpperCase() + randomRace.slice(1);
    spec.value = randomSpec.charAt(0).toUpperCase() + randomSpec.slice(1);
    if (factionChoice.value === "Doesn't matter") {
        faction.value = randomFaction;
    } else {
        faction.value = factionChoice.value;
    }
}
</script>

<template>
    <div>
        <h1>Wow Cataclysm Race/Class Randomizer</h1>
        <div class="chosen">
            <h2 class="faction">Faction: {{ faction }}</h2>
            <h2 class="race">Race: {{ race }}</h2>
            <h2 class="cclass">Class: {{ cclass }}</h2>
            <h2 class="spec">Spec: {{ spec }}</h2>
        </div>
        <h2>Options:</h2>
        <div class="form">
            <label for="faction">Faction:</label>
            <select v-model="factionChoice">
                <option>Doesn't matter</option>
                <option>Alliance</option>
                <option>Horde</option>
            </select>
        </div>
        <button class="generate" @click="generate">Generate</button>
    </div>
</template>

<style scoped></style>
