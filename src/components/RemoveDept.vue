<template>
    <v-dialog max-width="500px">
        <v-btn
            color="error"
            class="shadow-none ml-auto rounded-0 white--text"
            slot="activator"
            @click="dialog = true"
            >
            <v-icon left dark>mdi-trash-can-outline</v-icon>
            Delete Department
        </v-btn>
        <v-card>
        <v-card-title>
            <span class="headline">New Department</span>
        </v-card-title>
        <v-card-text>
            <v-container>
            <v-row>
                <v-col cols="12">
                <v-select
                  :items="['0-17', '18-29', '30-54', '54+']"
                  label="Age*"
                  required
                ></v-select>
                </v-col>
            </v-row>
            </v-container>
        </v-card-text>
        <v-card-actions>
            <v-spacer></v-spacer>
            <!-- <v-btn color="blue darken-1" text @click="dialog = false">Close</v-btn>
            <v-btn color="blue darken-1" text @submit.prevent="addDept()">Save</v-btn> -->
        </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
export default {
    data () {
        return {
            dialog: false,
        }
    }
}
</script>