<template>
   <v-container class=" d-flex justify-center">
       <v-card width="300">
           <v-col class="d-flex justify-center">
           <v-form @submit="validateDetails()">
               <v-col cols="12">
               <v-text-field v-model="fname" label="First Name"></v-text-field>
               </v-col>
               <v-col cols="12">
               <v-text-field v-model="sname" label="Second Name"></v-text-field>
               </v-col>
       
  <h3>Choose a means of transport</h3>

<input v-model="vehicle" type="checkbox" value="car">
<label for="car">Car</label><br>
<input v-model="vehicle" type="checkbox" value="boat">
<label  for="boat">Boat</label>
<h3>Choose a gender</h3>
<input type="radio"  name="gender" value="female" v-model="genderValue">
<label for="female">Female</label><br>
<input type="radio"  name="gender" value="male" v-model="genderValue">
<label for="other">Male</label>
<v-col>
 <v-btn type="submit"  depressed color="green">Submit</v-btn>
 </v-col>
           </v-form>
           </v-col>
           <v-btn @click="[displayData(), toggle =!toggle]" class="mb-4" >Load Submitted Names</v-btn>
           <p v-if="loading">Loading.....</p>
           <p>{{error}}</p>

           
               <h3>Welcome</h3>
               <div v-if="[!toggle, loading=!loading ]">
               <h3  :key="result.id" v-for="result in results" >  <h2 class="pink--text">{{result.loadName}} {{result.lastName}}</h2> </h3>
           </div>
       </v-card>

       
   </v-container>
</template>

<script>
    export default {
        name:'Form',
        methods:{
            displayData(){
                this.loading = true,
                fetch('https://vue-http-demo-e618d-default-rtdb.firebaseio.com/class.json')
                .then((response)=>{
                    if(response.ok){ return response.json()}
                })
                .then((data)=>{
                    this.loading = false;
                    const results = []
                    for(let id in data){
                        results.push({
                            id: id,
                            loadName: data[id].firstName,
                            lastName: data[id].secondName,
                            loadGender: data[id].gender,
                            loadVehicle: data[id].vehicle,
                        })
                    }
                    this.results = results;
                }).catch(()=>{
                    return this.error='there is an error'
                })
                
               
                
            },
            
            
            validateDetails(){
                fetch('https://vue-http-demo-e618d-default-rtdb.firebaseio.com/class.json',
                {
                    method:'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        firstName: this.fname,
                        secondName: this.sname,
                        gender: this.genderValue,
                        transport: this.vehicle,

                    })

                });
              
           
                if(this.fname === ''){
                    return alert('Enter your first name')
                } else if(this.sname === ''){
                   return alert('Enter your second Name')
                } else if (this.radioGroup === ''){
                    return alert('Choose a gender')
                } else if(this.vehicle === [])
                return alert('Choose a vehicle')
                else {return alert('Thank you for submitting');}
              
            },
        },
        data(){
            return{
                error: null,
                loading: false,
                toggle: false,
                fname:'',
                sname:'',
                genderValue:'',
                vehicle: [],
                results:[],
                
            }
        },
        mounted(){
            this.displayData();
        }
        
   

        
    }
    
</script>

<style lang="scss" scoped>

</style>