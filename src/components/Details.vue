<template>
  <div>
        <h1>This is the article number :  {{ $route.params.id }}</h1>
        <ul>
            <li v-for="show in showData" :value="show[3]">
                <h2>Title : {{ show[1] }}</h2>
                <h4>Desc : {{ show[0] }}</h4>
                <div v-for="showPhoto in showPhotos" >
                    <img :src="showPhoto[2]">                    
                </div>
            </li>
        </ul>
  </div>
</template>

<script>
export default {
  name: "Details",
  mounted(){
     this.url_data=this.$route.params.id;
  },
  data() {
    return {
        data:{

        },
        showData:[],
        showPhotos:[],
        url_data : null,
    };
  },
  beforeMount(){
        this.get(),
        this.photos()
  },
  methods:{
    async get(){
        const res = await fetch('https://jsonplaceholder.typicode.com/posts');
        const data = await res.json()
        this.data = data
        let all = [] 
        
           for(let i = data.length - 1; i >= 0; i--){
                let dataTable = [data[i]["body"], data[i]["title"], data[i]["id"], data[i]["userId"]]
                if(data[i]["id"] == this.url_data){
                    all.push(dataTable)
                    this.showData = all
                }
            }   
            console.log(this.showData)
    },
    async photos(){
        const res = await fetch('https://jsonplaceholder.typicode.com/photos');
        const data = await res.json()
        this.data = data
        let all = [] 
            for(let i = data.length - 1; i >= 0; i--){
                let dataTable = [data[i]["albumId"], data[i]["title"], data[i]["thumbnailUrl"], data[i]["url"]]
                if(data[i]["albumId"] == this.url_data){
                    all.push(dataTable)
                    this.showPhotos = all
                }
            }  
    },
  },
  
};
</script>
<style scoped>
p, h1, h2, h3, h4, h5, h6, span {
  font-family: "Roboto", sans-serif;
}
div{
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 50px
}
div h1 {
    margin-top: 20px;
}
div ul li {
    display : flex;
    flex-direction: column;
    align-items: center;
    gap:20px;
}
</style>
