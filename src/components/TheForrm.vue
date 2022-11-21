<script lang="ts">
interface Contact {
  name: string;
  email: string;
  checkedLocations: string[];
  employees: number;
}

interface ContactError {
  name?: string;
  email?: string;
  checkedLocations?: string;
  employees?: string;
}

export default {
  data() {
    return {
      form: {
        name: "",
        email: "",
        checkedLocations: [],
        employees: 0,
      },
      error: new Object() as ContactError,
      submitted: false,
      isSubmitting: false,
    };
  },
  methods: {
    handleEmployees(value: "add" | "sub") {
      if (value === "add") {
        return (this.form.employees += 1);
      }
      return (this.form.employees -= 1);
    },

    validate({ name, email, employees }: Contact) {
      this.error = new Object() as ContactError;
      let invalid = false;

      if (name.length <= 2) {
        invalid = true;
        this.error.name = "Por favor, informe seu nome completo.";
      }

      if (!/^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(email)) {
        invalid = true;
        this.error.email = "Por favor, informe seu melhor e-mail.";
      }

      if (employees < 0) {
        invalid = true;
        this.error.employees = "o número de funcionários precisa ser positivo";
      }

      return invalid;
    },

    timeout(ms: number) {
      return new Promise((resolve) => setTimeout(resolve, ms));
    },

    checkForm(e: any) {
      e.preventDefault();
      this.isSubmitting = true;
      if (this.validate(this.form)) {
        this.isSubmitting = false;
        return;
      }
      // criado para dar um tempo de loading
      this.timeout(2000).then(() => {
        this.isSubmitting = false;
        this.submitted = true;
        console.log(this.form);
      });
    },
  },
};
</script>

<script setup lang="ts">
import Loading from "./TheLoading.vue";
</script>

<template>
  <div class="container">
    <div class="item">
      <div class="details">
        Deixa aqui seus dados que entraremos em contato!
      </div>

      <form class="contact" @submit="checkForm">
        <label for="name">
          Nome Completo*
          <input id="name" v-model="form.name" required />
          <span v-if="error.name" class="error">{{ error.name }}</span>
        </label>

        <label for="email">
          E-mail*
          <input id="email" v-model="form.email" required />
          <span v-if="error.email" class="error">{{ error.email }}</span>
        </label>

        <div class="contact--checkbox">
          Onde nos conheceu?
          <label for="google">
            <input
              type="checkbox"
              id="google"
              value="google"
              v-model="form.checkedLocations"
            />
            Google
          </label>

          <label for="social">
            <input
              type="checkbox"
              id="social"
              value="social"
              v-model="form.checkedLocations"
            />
            Redes Sociais
          </label>

          <label for="indication">
            <input
              type="checkbox"
              id="indication"
              value="indication"
              v-model="form.checkedLocations"
            />
            Indicação
          </label>

          <span v-if="error.checkedLocations" class="error">{{
            error.checkedLocations
          }}</span>
        </div>

        <div class="contact--employees">
          <label for="employees">Quantos de funcionários</label>
          <div>
            <button type="button" @click="handleEmployees('add')">+</button>
            <input
              id="employees"
              name="employees"
              v-model="form.employees"
              type="number"
            />
            <button
              type="button"
              :disabled="form.employees <= 0"
              @click="handleEmployees('sub')"
            >
              -
            </button>
          </div>
          <span v-if="error.employees" class="error">{{
            error.employees
          }}</span>
        </div>

        <div class="contact--actions">
          <button v-if="!submitted" :disabled="isSubmitting" type="submit">
            <span v-if="!isSubmitting">Enviar</span>
            <loading v-if="isSubmitting" />
          </button>
          <div v-if="submitted" class="success">
            Sua mensagem foi enviada com sucesso!
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 100%;
}

.item {
  position: relative;
  padding: 0 15px;
  display: flex;
  flex-direction: column;
  text-align: center;
}

.details {
  color: var(--white);
  font-size: 1.875rem;
  line-height: 2.813rem;
  max-width: 412px;
  text-align: center;
  margin: 60px auto;
}

.contact {
  display: flex;
  flex-direction: column;
  text-align: left;
  max-width: 412px;
  width: 100%;
  margin: 0 auto;
  padding: 0 10px;
}

.contact label {
  color: var(--white);
  margin-bottom: 30px;
  font-size: 1.25rem;
  line-height: 1.875rem;
}

.contact label input {
  color: var(--gray);
  font-size: 1.25rem;
  line-height: 1.875rem;
  height: 65px;
  margin-top: 20px;
  width: 100%;
  padding: 15px;
}

.contact .contact--actions {
  width: 100%;
  margin: 10px auto 60px;
}

.contact .contact--checkbox {
  display: flex;
  flex-direction: column;
  color: var(--white);
  font-size: 1.25rem;
  line-height: 1.875rem;
  margin-bottom: 30px;
}

.contact .contact--checkbox label {
  display: flex;
  align-items: center;
  margin: 20px 0 0;
}

.contact .contact--checkbox label input {
  width: 30px;
  height: 23px;
  margin: 0 13px 0 0;
}

.contact .contact--employees div {
  display: flex;
  align-items: center;
  margin: 20px 0;
}

.contact .contact--employees div input {
  width: 70px;
  height: 40px;
  font-size: 1.25rem;
  line-height: 1.875rem;
  border: none;
  margin: 0 15px;
  padding: 5px;
  text-align: center;
}

.contact .contact--employees div button {
  width: 50px;
  height: 40px;
}

.contact .contact--actions button {
  width: 100%;
  height: 65px;
}

@media screen and (min-width: 915px) {
  .container {
    width: 50%;
  }

  .item {
    max-width: 640px;
    height: 100%;
    margin: 0 auto 0 0;
    box-shadow: 0 0 15px 0px rgba(0, 0, 0, 0.25);
    clip-path: inset(0px -15px 0px -15px);
  }
}
</style>
