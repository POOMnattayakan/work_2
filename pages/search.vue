<template>
  <v-form v-model="valid">
    <v-text-field
      v-model="member"
      :rules="memberRules"
      label="กรอกข้อมูล"
      required
     ></v-text-field>
     <v-btn color="primary" dark @click="Dosearch">ค้นหา
        <v-icon dark right>label</v-icon>
      </v-btn>
      <v-btn color="success" dark @click="Doclean">ล้างข้อมูล
        <v-icon dark right>label</v-icon>
      </v-btn>
      <div>
  <v-data-table
    :headers="headers"
    :items="desserts"
    class="elevation-1"
  >
    <template slot="items" slot-scope="props">
     <td>{{ props.item.cid }}</td>
      <td class="text-xs-center">{{ props.item.cname }}</td>
      <td class="text-xs-center">{{ props.item.color }}</td>
      <td class="text-xs-center">{{ props.item.price }}</td>
      
    </template>
    
    <template slot="pageText" slot-scope="props">
      Lignes {{ props.pageStart }} - {{ props.pageStop }} de {{ props.itemsLength }}
    
    </template>
  </v-data-table>
   <div>
    <v-btn color="success">เพิ่ม</v-btn>
    <v-btn color="warning">แก้ไข</v-btn>
    <v-btn color="error">ลบ</v-btn>
    </div>
  </div>
  </v-form>
</template>

<script>
export default {
  data () {
  return {
      headers: [
        {
          text: 'cid',
            align: 'left',
            sortable: false,
            value: 'name'
          },
          { text: 'cname', value: 'cname', align: 'center' },
          { text: 'color', value: 'color', align: 'center' },
          { text: 'price', value: 'price', align: 'center' },
      ],
      desserts: [],
      member :'',
    };
  },
  async created() {
   this.getstudent()     
  },
  methods: {
    async Dosearch() {
      console.log(this.member);
      let res = await this.$http.post("http://127.0.0.1/php-test/search.php?name="+this.member)
        this.desserts = res.data.admin
    },
    async getstudent() {
      let res = await this.$http.get('http://127.0.0.1/php-test/list-student.php')
      this.desserts = res.data.student
    },
    async Doclean() {
      let res = await this.$http.get('http://127.0.0.1/php-test/list-student.php')
      this.member ='',
      this.getstudent() 
    },
  }
  
}

</script>