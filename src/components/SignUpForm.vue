<template>
  <div>
    <h2>Form Projesi</h2>
    <form @submit.prevent="handleSubmit()">
      <label>E mail:</label>
      <input type="email" v-model="email" required />

      <label>Şifre</label>
      <input type="password" v-model="password" required />
      <div class="passwordError" v-if="passwordError">
        {{ passwordError }}
      </div>

      <label>Cinsiyet:</label>
      <select v-model="gender">
        <option value="male">Erkek</option>
        <option value="female">Kadın</option>
      </select>
      <label>Bildiğiniz Yazılım Dilleri:</label>
      <input type="text" v-model="skill" @keyup.alt="addSkill($event)" />
      <div v-for="skillItem in skills" :key="skillItem" class="skillItem">
        <span @click="deleteSkill(skillItem)">{{ skillItem }}</span>
      </div>
      <div class="term">
        <input class="termInput" v-model="term" type="checkbox" required />
        <label>Kullanım koşullarını kabul ediyorum</label>
      </div>

      <div class="btnDiv">
        <button>Kayıt Ol</button>
      </div>
    </form>

    <p>{{ email }}</p>
    <p>{{ password }}</p>
    <p>{{ gender }}</p>
    <p>{{ term }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      gender: "",
      term: false,
      skill: "",
      passwordError: null,

      skills: [],
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.skill) {
        if (!this.skills.includes(this.skill)) {
          this.skills.push(this.skill);
        }
        this.skill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((x) => {
        return skill !== x;
      });
    },
    handleSubmit() {
      this.passwordError =
        this.password.lenght > 5
          ? ""
          : "Lütfen minimum 6 karakterli bir şifre giriniz";

      console.log("Email ", this.email);
      console.log("Şifre ", this.password);
      console.log("Cinsiyet ", this.gender);
      console.log("Koşullar ", this.term);
      console.log("Yetenekler ", this.skills);
    },
  },
};
</script>

<style>
form {
  max-width: 450px;
  width: 100%;
  background: antiquewhite;
  padding: 40px;
  border-radius: 20px;
  margin: 40px auto;

  text-align: left;
}
input,
select {
  display: block;
  width: 100%;
  padding: 10px 8px;
  border-radius: 24px;
  border: none;
  outline: none;
}
label {
  margin: 15px 10px;
  display: inline-block;
  font-size: 18px;
  font-weight: bold;
  letter-spacing: 2px;
}
.termInput {
  width: 16px;
}
.term {
  display: flex;
  align-items: center;
}
button {
  font-size: 18px;
  padding: 10px 20px;
  border: none;
  border-radius: 15px;
  background: green;
  color: white;
}
.skillItem {
  background-color: white;
  margin: 20px 10px;
  display: inline-block;
  color: green;
  padding: 8px 10px;
  border-radius: 20px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.passwordError {
  color: red;
  margin-top: 10px;
  font-size: 15px;
  font-weight: bold;
  letter-spacing: 1px;
}
</style>
