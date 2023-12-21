<template>
    <v-app style="background-color: #ECEFF1">
        <v-container class="container">
            <v-card>
                <h1>Age Calculator</h1>
                <div class="calculate">
                    <v-row>
                        <v-col cols="12" md="8">
                            <v-text-field v-model="inputDate" variant="outlined" type="date"></v-text-field>
                        </v-col>
                        <v-col cols="12" md="4">
                            <v-btn @click="calculateAge()" variant="text" color="blue">Calculate</v-btn>
                        </v-col>
                        <h4 v-if="ageCalculated">Umur kamu sekarang adalah <span>{{ y3 }}</span> tahun, <span>{{ m3
                        }}</span> bulan, <span>{{ d3 }}</span> hari
                        </h4>
                    </v-row>
                    <v-btn @click="clear()" style="margin-top: 3rem;" variant="text" color="red">Clear</v-btn>
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

            this.y3 = y2 - y1;

            if (m2 >= m1) {
                this.m3 = m2 - m1;
            } else {
                this.y3--;
                this.m3 = 12 + m2 - m1;
            }

            if (d2 >= d1) {
                this.d3 = d2 - d1;
            } else {
                this.m3--;
                this.d3 = this.getDaysInMonth(y1, m1) + d2 - d1;
            }

            if (this.m3 < 0) {
                this.m3 = 11;
                this.y3--;
            }

            this.ageCalculated = true;
        },
        getDaysInMonth(year, month) {
            return 32 - new Date(year, month, 0).getDate();
        },
        clear() {
            this.inputDate = new Date().toISOString().substr(0, 10);
            this.y3 = null;
            this.m3 = null;
            this.d3 = null;
            this.ageCalculated = false;
        }
    }
}
</script>

<style>
.container {
    margin-top: 3rem;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.v-card {
    max-width: 600px;
    /* Lebar maksimal untuk card */
    width: 100%;
    /* Lebar full pada ukuran layar kecil */
}

h1 {
    margin-top: 2rem;
    /* margin-bottom: 1rem; */
    /* text-align: center; */
    padding-left: 3rem;
    font-weight: bold;
}

h4 {
    padding-left: 1rem;
}

h4 span {
    color: #5E747F;
}

.calculate {
    padding: 1rem;
    margin-top: 2rem;
    /* margin-bottom: 2rem; */
    /* text-align: center; */
}

@media (min-width: 600px) {
    .calculate {
        padding: 3rem;
    }
}
</style>