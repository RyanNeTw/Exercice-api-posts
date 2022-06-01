<template>
  <div>
    <ul>
        <li v-for="show in showData">
            <h2>{{ show[1] }}</h2>
            <h4>{{ show[0] }}</h4>
            <button v-on:click="photos(show[3])" v-if="show[3] != null" :value="show[3]">Pictures {{ show[3] }}</button>
            <button v-on:click="photos()" v-if="show[3] != null" :value="show[3]">Hide</button>
            <a :href="'/#/' + show[2]">Show Details</a>
            <p @click="like()">Like <span v-if="!isNaN(likes)">{{ likes }}</span> click to like</p>
            <div class="imgtot" v-for="showPhoto in showPhotos">
                <img :src="showPhoto[2]">                    
            </div>
        </li>   
    </ul>

  </div>
</template>

<script>
export default {
  name: "Posts",
  data() {
    return {
        data:{

        },
        showData:[],
        showPhotos:[],
        likes : parseInt(localStorage.getItem("likes")),
    };
  },
  beforeMount(){
        this.get(),
        this.photos()
  },
  methods:{
    like : function(){
        this.likes += 1
        if(this.likes > 0){
            localStorage.setItem("likes", this.likes)
        }else{
            this.likes = 1
        }
    },
    async get(){
        const res = await fetch('https://jsonplaceholder.typicode.com/posts');
        const data = await res.json()
        this.data = data
        let all = [] 
        
        console.log(data)
           for(let i = data.length - 1; i >= 0; i--){
                let dataTable = [data[i]["body"], data[i]["title"], data[i]["id"], data[i]["userId"]]
                all.push(dataTable)
                this.showData = all
            }   
    },
      async photos(number){
        const res = await fetch('https://jsonplaceholder.typicode.com/photos');
        const data = await res.json()
        this.data = data
        let all = [] 
        if(number != null){
            for(let i = data.length - 1; i >= 0; i--){
                let dataTable = [data[i]["albumId"], data[i]["title"], data[i]["thumbnailUrl"], data[i]["url"]]
                if(data[i]["albumId"] == number){
                    all.push(dataTable)
                    this.showPhotos = all
                }
            }  
        }else{
            this.showPhotos = []
        }
    },
  },
  
};
</script>
<style scoped>
p, h1, h2, h3, h4, h5, h6, span {
  font-family: "Roboto", sans-serif;
}
ul {
   display: flex;
   flex-direction: column;
   gap: 50px;
}
ul li{
    display: flex;
    flex-direction: column;
    gap: 10px;
    border: 1px solid black;
    padding: 10px 0px 10px 0px;
}
ul li  h2{
    font-size:18px;
    align-self: center;
}
ul li  h4{
    font-size: 10px;
    align-self: center;
}
ul li  div{
    display:flex;
    flex-direction: row;
    border: none
}
ul li a {
    align-self: center;
}
ul li p {
    align-self: center;
}
ul li  img{
    width: 50px;
}
</style>
