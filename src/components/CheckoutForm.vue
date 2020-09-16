<template>
    <form class="checkout-form" v-on:submit.prevent="submit">
        <div class="row">
            <div class="col-12 form-group">
                <label class="col-form-label col-form-label-lg">Full Name <span class="text-danger">*</span></label>
                <input type="text" v-model.trim="$v.fullname.$model" :class="{'is-invalid': validationStatus($v.fullname)}" class="form-control form-control-lg">
                <div v-if="!$v.fullname.required" class="invalid-feedback">The full name field is required.</div>
            </div>
            <div class="col-12 form-group">
                <label class="col-form-label col-form-label-lg">Email <span class="text-danger">*</span></label>
                <input type="email" v-model.trim="email" :class="{'is-invalid': validationStatus($v.email)}" class="form-control form-control-lg">
                <div v-if="!$v.email.required" class="invalid-feedback">The email field is required.</div>
                <div v-if="!$v.email.email" class="invalid-feedback">The email field is not valid'.</div>
            </div>
            <div class="col-6 form-group">
                <label class="col-form-label col-form-label-lg">Country <span class="text-danger">*</span></label>
                <select v-model.trim="country" :class="{'is-invalid': validationStatus($v.country)}" class="form-control form-control-lg">
                    <option value="">Select Country</option>
                    <option v-for="c in countryList" :value="c.code" :key="c.code">{{ c.name }}</option>
                </select>
                <div v-if="!$v.country.required" class="invalid-feedback">The country field is required.</div>
            </div>
            <div class="col-6 form-group">
                <label class="col-form-label col-form-label-lg">City <span class="text-danger">*</span></label>
                <input  type="text" v-model.trim="city" :class="{'is-invalid': validationStatus($v.city)}" class="form-control form-control-lg">
                <div v-if="!$v.city.required" class="invalid-feedback">The city field is required.</div>
            </div>
            <div class="col-12 form-group">
                <label class="col-form-label col-form-label-lg">Address <span class="text-danger">*</span></label>
                <input type="text" v-model.trim="address" :class="{'is-invalid': validationStatus($v.address)}" class="form-control form-control-lg">
                <div v-if="!$v.address.required" class="invalid-feedback">The address field is required.</div>
            </div>
            <div class="col-6 form-group">
                <label class="col-form-label col-form-label-lg">Postal Code</label>
                <input  type="text" v-model.trim="postalCode" class="form-control form-control-lg">
            </div>
            <div class="col-6 form-group">
                <label class="col-form-label col-form-label-lg">Phone <span class="text-danger">*</span></label>
                <input  type="tel" v-model.trim="phone" :class="{'is-invalid': validationStatus($v.phone)}" class="form-control form-control-lg">
                <div v-if="!$v.phone.required" class="invalid-feedback">The phone number field is required.</div>
            </div>
            <div class="col-12 form-group text-center">
                <button class="btn btn-vue btn-lg col-5">Go to payment</button>
            </div>
        </div>
    </form>
</template>

<script>
    import { required, email} from 'vuelidate/lib/validators'
    export default {
        name: "CheckoutForm",
        data: function () {
            return {
                fullname: '',
                email: '',
                address: '',
                country: '',
                countryList: [],
                city: '',
                postalCode: '',
                phone: ''
            }
        },
        validations: {
            fullname: {required},
            email: {required, email},
            address: {required},
            country: {required},
            city: {required},
            postalCode: {required},
            phone: {required},
        },

        mounted: function() {
            let v = this;
            v.$http.get(`http://localhost:4600/countries`)
                .then(function (resp) {
                    v.countryList = resp.data;
                })
                .catch(function (err) {
                    console.log(err);
                })
        },
        methods: {

            resetData: function() {
                this.fullname = '';
                this.email = '';
                this.address = '';
                this.country = '';
                this.city = '';
                this.postalCode = '';
                this.phone = '';

            },

            validationStatus: function(validation) {
                return typeof validation != 'undefined' ? validation.$error : false;
            },
            submit: function () {
                this.$v.$touch();
                if(this.$v.$pendding || this.$v.$error) return;

                this.$v.$reset();
                this.resetData();

            }
        }
    }
</script>

<style scoped>
    .btn-vue {
        background: #53B985;
        color: #31485D;
        font-weight: 700;
    }

</style>
