<template>
    <v-container>


        <v-row>
            <v-text-field @keyup.enter="addMember" v-model="textInput" autofocus clearable maxlength="30"
                          class="smaller"/>
            <v-btn icon @click="addMember">
                <v-icon>mdi-plus</v-icon>
            </v-btn>
        </v-row>
        <v-btn @click="setHighlighted">
            Choose Random
        </v-btn>
        <p/>
        <v-row child-flex>
            <v-layout>
                <v-list>

                    <v-list-item v-for="(member, index) in members" :key="index" class="mt-2 mb-2"
                                 :class="isHighlighted(member) ? 'selected': 'transparent'">
                        <v-col>
                            <v-list-item-title>{{ member.text }}</v-list-item-title>
                        </v-col>
                        <v-col>
                            <v-btn @click="deleteMember(index)" class="delete-button">X</v-btn>
                        </v-col>
                    </v-list-item>
                </v-list>
            </v-layout>
        </v-row>
    </v-container>
</template>

<script>

export default {
    data() {
        return {
            textInput: "",
            members: [],

        }
    },
    methods: {
        addMember() {
            this.textInput = this.textInput.trim();
            if (!this.textInput) return;
            this.members.push({text: this.textInput, highlight: false});
            this.textInput = '';
        },
        isHighlighted(member) {
            return member.highlight;
        },
        setHighlighted() {
            const idx = Math.floor(Math.random() * this.members.length);
            this.members.forEach(d => d.highlight = false);
            this.members[idx].highlight = true;
        },
        deleteMember(index) {
            this.members.splice(index, 1);
        }
    },
    mounted() {
        this.members.pop();
    }

}
</script>
<style>
* {
    font-size: 14px;
}

.selected {
    background-color: green;
}

.delete-button {
    /*color: #0055ff !important;*/
    /*background-color: transparent !important;*/
}

.smaller {
    width: 50%;
    align-self: start;
    float: left;
}
</style>
