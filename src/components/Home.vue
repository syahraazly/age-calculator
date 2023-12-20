<template>
    <v-app style="background-color: #263238;">
        <v-container>
            <h1>Age Calculator</h1>
            <v-card class="container">
                <div class="calculate">
                    <v-row>
                        <v-col cols="12" md="8">
                            <v-text-field v-model="inputDate" variant="outlined" type="date"></v-text-field>
                        </v-col>
                        <v-col cols="12" md="4">
                            <v-btn @click="calculateAge">Calculate</v-btn>
                        </v-col>
                        <h2 v-if="ageCalculated">Umur kamu sekarang adalah {{ y3 }} tahun, {{ m3 }} bulan, {{ d3 }} hari
                        </h2>
                    </v-row>
                </div>
            </v-card>
        </v-container>
    </v-app>
</template>

<script>
export default {
    name: 'Home',
    data() {
        return {
            inputDate: new Date().toISOString().substr(0, 10),
            y3: null,
            m3: null,
            d3: null,
            ageCalculated: false
        };
    },
    methods: {
        calculateAge() {
            let birthDate = new Date(this.inputDate);
            let today = new Date();

            let d1 = birthDate.getDate();
            let m1 = birthDate.getMonth();
            let y1 = birthDate.getFullYear();

            let d2 = today.getDate();
            let m2 = today.getMonth();
            let y2 = today.getFullYear();

            let d3, m3, y3;

            y3 = y2 - y1;

            if (m2 >= m1) {
                m3 = m2 - m1;
            } else {
                y3--;
                m3 = 12 + m2 - m1;
            }

            if (d2 >= d1) {
                d3 = d2 - d1;
            } else {
                m3--;
                d3 = getDaysInMonth(y1, m1) + d2 - d1;
            }

            if (m3 < 0) {
                m3 = 11;
                y3--;
            }
        },
        getDaysInMonth(year, month) {
            return 32 - new Date(year, month, 0).getDate();
        }
    }


}
</script>

<style>
.container {
    margin-top: 3rem;
    text-align: center;
}

h1 {
    margin-top: 2rem;
    margin-bottom: 2rem;
    color: #ECEFF1;
    text-align: center;
}

.calculate {
    padding: 3rem;
    margin-top: 2rem;
    margin-bottom: 2rem;
}
</style>