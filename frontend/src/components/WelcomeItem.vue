<template>
  <div class="formbold-main-wrapper">
  <div class="formbold-form-wrapper">
    
    <form>
      <div class="formbold-form-title">
        <h2 class="">Créer une tâche</h2>
        <p>
          Veuillez renseigner les informations nécessaires pour l'enregistrement
        </p>
      </div>

      <div class="formbold-mb-3">
        <label for="title" class="formbold-form-label">
          Title
        </label>
        <input
          type="text"
          name="title"
          id="title"
          class="formbold-form-input"
          v-model="title"
        />
      </div>

      <div class="formbold-mb-3">
        <label for="description" class="formbold-form-label">
          Description
        </label>
        <input
          type="text"
          name="description"
          id="description"
          class="formbold-form-input"
          v-model="description"
        />
      </div>

      <div v-if="todo" class="formbold-mb-3">
        <div>
          <label for="status" class="formbold-form-label"> Status </label>
          <select
            name="status"
            id="status"
            class="formbold-form-input"
            v-model="status"
          >
          <option
          value="pending"
          > En attente</option>
          <option
          value="in progress"
          > En cours</option>
          <option
          value="closed"
          > Terminées</option>
          <option
          value="archived"
          > Archivées</option>

        </select>
        </div>  
      </div>

<div class="formbold-btn">

  <button type="button" class="formbold-btn1" @click="submitForm" >Enregistrer</button>
  <button class="formbold-btn2" @click="$router.push('/')" >Cancel</button>
  
</div>
    </form>
  </div>
</div>
</template>


<script>
import axios from 'axios';

export default {
  data () {
    return {
      title: "",
      description: "",
      status: "",
      todo: null
    }
  },
  async beforeMount() {
    try {
      const id = this.$route.params.id;
      if(id && !isNaN(id)) {
        const response = await axios.get("http://localhost:3000/todos/" + id);
        this.todo = response.data;
        this.title = response.data.title;
        this.description = response.data.description;
        this.status = response.data.status;
      }
    } catch (error) {
      console.log(error)
    }
  },
  methods: {
    submitForm () {
      if(this.todo) {
        axios.patch("http://localhost:3000/todos/" + this.todo.id, {
          title: this.title,
          description: this.description,
          status: this.status
        })
        .then((response) => {
          this.$router.push('/')
        })
        .catch(function (error) {
          console.log(error);
        });
      } else {
        axios.post("http://localhost:3000/todos", {
        title: this.title,
        description: this.description
        })
        .then((response) => {
          // console.log(response);
          this.title = "";
          this.description = "";
          this.$router.push('/')
        })
        .catch(function (error) {
          console.log(error);
        });
      }
    }
  }
}
</script>


<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    border-radius: 15px;
  }
  body {
    font-family: 'Inter', sans-serif;
  }
  .formbold-mb-3 {
    margin-bottom: 15px;
  }
  .formbold-relative {
    position: relative;
  }
  .formbold-opacity-0 {
    opacity: 0;
  }
  .formbold-stroke-current {
    stroke: currentColor;
  }
  #supportCheckbox:checked ~ div span {
    opacity: 1;
  }

  .formbold-main-wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 48px;
  }

  .formbold-form-wrapper {
    margin: 0 auto;
    max-width: 570px;
    width: 100%;
    background: white;
    padding: 40px;
  }

  .formbold-img {
    margin-bottom: 45px;
  }

  .formbold-form-title {
    margin-bottom: 30px;
    text-align: center;
  }
  .formbold-form-title h2 {
    font-weight: 600;
    font-size: 28px;
    line-height: 34px;
    color: #07074d;
  }
  .formbold-form-title p {
    font-size: 16px;
    line-height: 24px;
    color: #536387;
    margin-top: 12px;
  }

  .formbold-input-flex {
    display: flex;
    gap: 20px;
    margin-bottom: 15px;
  }
  .formbold-input-flex > div {
    width: 50%;
  }
  .formbold-form-input {
    text-align: center;
    width: 100%;
    padding: 13px 22px;
    border-radius: 5px;
    border: 1px solid #dde3ec;
    background: #ffffff;
    font-weight: 500;
    font-size: 16px;
    color: #536387;
    outline: none;
    resize: none;
  }
  .formbold-form-input:focus {
    border-color: #6a64f1;
    box-shadow: 0px 3px 8px rgba(0, 0, 0, 0.05);
  }
  .formbold-form-label {
    color: #536387;
    font-size: 14px;
    line-height: 24px;
    display: block;
    margin-bottom: 10px;
  }

  .formbold-checkbox-label {
    display: flex;
    cursor: pointer;
    user-select: none;
    font-size: 16px;
    line-height: 24px;
    color: #536387;
  }
  .formbold-checkbox-label a {
    margin-left: 5px;
    color: #6a64f1;
  }
  .formbold-input-checkbox {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border-width: 0;
  }
  .formbold-checkbox-inner {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 20px;
    height: 20px;
    margin-right: 16px;
    margin-top: 2px;
    border: 0.7px solid #dde3ec;
    border-radius: 3px;
  }

  .formbold-btn1 {
    font-size: 16px;
    border-radius: 5px;
    padding: 14px 25px;
    border: none;
    font-weight: 500;
    background-color: #6a64f1;
    color: white;
    cursor: pointer;
    margin-top: 25px;
  }
  .formbold-btn2 {
    font-size: 16px;
    border-radius: 5px;
    padding: 14px 25px;
    border: none;
    font-weight: 500;
    background-color: #840404;
    color: white;
    cursor: pointer;
    margin-top: 25px;
    /* margin-left: 25px; */
  }
  .formbold-btn1:hover {
    box-shadow: 0px 3px 8px rgba(0, 0, 0, 0.05);
  }

  .formbold-btn2:hover {
    box-shadow: 0px 3px 8px rgba(0, 0, 0, 0.05);
  }

  .formbold-btn{
    display: flex;
    justify-content: space-between;
  }
</style>

