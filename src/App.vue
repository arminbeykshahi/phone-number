<template>
  
  <div class="main mt-5">
    <div class="container">
      <div class="row">
        <div class="col-md-6 mx-auto">
          <div class="alert alert-danger" v-if="namayeshalert">
             لطفا تمامی فیلد ها را پر کنید
          </div>

      
            <form @submit.prevent="validation">

             <div class="mb-4">
             <label for="name" class="form-label">نام : </label>
             <input type="text" v-model="name" class="form-control" id="name" placeholder="نام خود را وارد کنید...">
             </div>

             <div class="mb-5">
             <label for="number" class="form-label">شماره همراه : </label>
             <input type="text" v-model="number" class="form-control" id="number" placeholder="لطفا شماره خود را وارد کنید...">
             </div>

             <button  type="submit" class="btn btn-success w-100">ارسال</button>

             </form>
             
             <br>
             <br>
             <br>
             <hr>
             <h4>نمایش نتیجه :</h4>

             <form @submit.prevent="showresult">
             <input type="text" v-model="meghdar"  class="form-control w-100 mt-3" placeholder="نام مورد نظر را وارد کنید ...">
             <p v-if="namayeshnatije" class="text-danger">لطفا فیلد را پر کنید</p>
             <button type="submit" class="btn btn-primary mt-3 w-100">جستجو</button>
             </form>

             <ul class="mt-5">
              <li class="d-flex justify-content-between align-items-center"  v-for=" result in results" :key="result.id">
                <div>{{result.name}}</div>
                <div>{{result.phonenumber}}</div>
              </li>
             </ul>
            

        
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import { reactive, ref } from 'vue'


export default {

  setup() { 

  const name = ref('')
  const number = ref('')
  const namayeshalert = ref(false)
  const users = ref([])
  const meghdar = ref('')
  const results = ref([])
  const namayeshnatije = ref(true)


  

  function validation() {

     if (name.value !== '' || number.value !== '') {

       namayeshalert.value = false

        const userinfo = reactive({
        name : name.value,
        phonenumber : number.value

         })


         users.value.push(userinfo)

         console.log(users.value);
      
     }

     else {

         namayeshalert.value = true
     }
    
    
  }
  
 
  validation()


  function showresult() {

    if (meghdar.value != '') {

       results.value = users.value.filter(user=>user.name == meghdar.value)
       namayeshnatije.value = false
      
    } else {

      namayeshnatije.value = true
      
    }

   
      
     

  }

    showresult()

 


  

    return {name,number,namayeshalert,users,validation,showresult,meghdar,results,namayeshnatije}
  }
 
}
</script>

<style>

  html {

     direction: rtl !important;
    
  }


  

</style>
