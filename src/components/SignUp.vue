<template>
  <form class="sign-up" @submit.prevent="checkForm">
    <div class="form-group">
      <label for="name">Имя:</label>
      <input
        id="name"
        class="form-control"
        :class="$v.form.name.$error ? 'is-invalid' : ''"
        v-model.trim="form.name"
      >
      <p v-if="$v.form.name.$dirty && !$v.form.name.required" class="invalid-feedback">
        Введите имя
      </p>
      <p v-if="$v.form.name.$dirty && !$v.form.name.minLength" class="invalid-feedback">
        Здесь должно быть больше 3-и символов
      </p>
    </div>
  
    <div class="form-group">
      <label for="surname">Фамилия:</label>
      <input
        id="surname"
        class="form-control"
        :class="$v.form.surname.$error ? 'is-invalid' : ''"
        v-model.trim="form.surname"
      >
      <p v-if="$v.form.surname.$dirty && !$v.form.surname.required" class="invalid-feedback">
      Введите фамилие
      </p>
      <p v-if="$v.form.surname.$dirty && !$v.form.surname.minLength" class="invalid-feedback">
        Здесь должно быть больше 3-и символов
      </p>
    </div>

     <div class="form-group">
      <label for="patronymic">Отчество:</label>
      <input
        id="patronymic"
        class="form-control"
        :class="$v.form.patronymic.$error ? 'is-invalid' : ''"
        v-model.trim="form.patronymic"
      >
    </div>

       <div class="form-group">
      <label for="birth-date">Дата рождения:</label>
      <input
        id="birth-date"
        class="form-control"
        type="date"
        :class="$v.form.birthDate.$error ? 'is-invalid' : ''"
        v-model.trim="form.birthDate"
      >
      <p v-if="$v.form.birthDate.$dirty && !$v.form.birthDate.required" class="invalid-feedback">
       Введите дату рождения
      </p>
    
    </div>

        <div class="form-group">
      <label for="phone">Номер телефона:</label>
      <input
        id="phone"
        class="form-control"
        type="number"
        :class="$v.form.phone.$error ? 'is-invalid' : ''"
        v-model.trim="form.phone"
      >
      <p v-if="$v.form.phone.$dirty && !$v.form.phone.required" class="invalid-feedback">
        Введите номер телефона
      </p>
      <p v-if="$v.form.phone.$dirty && !$v.form.phone.minLength" class="invalid-feedback">
       Введите 11 цифр
      </p>
    </div>

    <div class="flex">
      <div class="form-check" :class="$v.form.gender.$error ? 'is-invalid' : ''">
        <input class="form-check-input" type="radio" value="male" name="exampleRadios" id="male" v-model="form.gender" >
        <label class="form-check-label" for="male">
          Мужчина
        </label>
      </div>
      <div class="form-check">
        <input class="form-check-input" type="radio" value="female" name="exampleRadios" id="female" v-model="form.gender">
        <label class="form-check-label" for="female">
          Женщина
        </label>
      </div>
    
        <p v-if="$v.form.gender.$dirty && !$v.form.gender.required" class="invalid-feedback">
        Выберите пол
      </p>
      
     
    </div>
    <button type="submit" class="btn btn-primary">Сохранить</button>
  </form>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength } from 'vuelidate/lib/validators'

export default {
  mixins: [validationMixin],
  data() {
    return {
      form: {
        name: '',
        surname: '',
        patronymic: '',
        birthDate:'',
        phone:'',
        gender:''
      },
    }
  },
  validations: {
    form: {
      name: { required,minLength: minLength(3)},
      surname: { required,minLength: minLength(3) },
      patronymic: {  },
      birthDate:{required},
      phone:{required,minLength:minLength(11)},
       gender:{required}
    }
  },
  methods: {
    checkForm() {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        alert('Валидация прошла успешно')
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.sign-up{
  width: 35%;
  margin: 0 auto;
}
.form-control {
  width: 400px;
}
.form-check {
  margin-right: 10px;
}
button {
  margin-top: 15px;
}
</style>