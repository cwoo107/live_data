<template>
  <div id="app">
    
    <b-container fluid>
      <div v-if="this.yesterday == null" class="d-lg-block">
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              <div class="spinner-border text-info" role="status" style='width: 3rem; height: 3rem;'>
                <span class="sr-only">Loading...</span>
              </div>
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
              &nbsp; <p />
      </div>
      <div v-else >
      <b-row >
        <b-col cols='2' class='float-left d-none d-lg-block'>
          <b-img src='./src/assets/usanorthlogo.png' width='600px' />
        </b-col>
        
        <b-col xl='8' lg='12'>
          <div style='padding-top: 25px'>
          <h2>
          Total Tickets: {{(total[0].total + total[1].total).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}  -  {{((total[0].total/(total[0].total + total[1].total))*100).toString().slice(0,5)}}% Web </h2>
          <h4>Express Tickets: {{sat[0].total}}</h4>
          Yesterday: {{(yesterday[0].total + yesterday[1].total).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}} Tickets  -  {{((yesterday[0].total/(yesterday[0].total + yesterday[1].total))*100).toString().slice(0,5)}}% Web 
          </div>
        </b-col>
        <b-col cols='2' class='d-none d-lg-block'>
          
          <div style=''>
          <h1 ><a >{{myDate}}</a> </h1>
          
          </div>
        </b-col>
      </b-row>
      <div class="d-none d-lg-block"> 
    <b-carousel
      id="carousel-fade"
      fade
      :interval="10000"
      controls
      indicators
      background="#212529"
      height='50px'
      img-width="1024"
      img-height="440"
      style="text-shadow: 1px 1px 2px #333;"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd"
    >

    <b-carousel-slide id='slide_1' img-blank img-alt="Blank image">
      <h3>Year to Date</h3>
        <b-row style='padding-bottom:50px;height: 550px'>
        <b-col md='12' >
          <div>
            <h4>{{(ytd[0].total + ytd[1].total).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}} Tickets - {{((ytd[1].total/(ytd[0].total + ytd[1].total))*100).toString().slice(0,5)}}% Web</h4>
            <b-table striped hover dark :items="ytd"></b-table>
          </div>
        </b-col>
        </b-row>
        <b-row>
          
        <b-col  md='12' style='margin-top:-350px'>
          <span v-if="month[12]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total],[month[8].name, month[8].total],[month[9].name, month[9].total],[month[10].name, month[10].total],[month[11].name, month[11].total],[month[12].name, month[12].total]]"></column-chart></span>
          <span v-else-if="month[11]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total],[month[8].name, month[8].total],[month[9].name, month[9].total],[month[10].name, month[10].total],[month[11].name, month[11].total]]"></column-chart></span>
          <span v-else-if="month[10]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total],[month[8].name, month[8].total],[month[9].name, month[9].total],[month[10].name, month[10].total]]"></column-chart></span>
          <span v-else-if="month[9]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total],[month[8].name, month[8].total],[month[9].name, month[9].total]]"></column-chart></span>
          <span v-else-if="month[8]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total],[month[8].name, month[8].total]]"></column-chart></span>
          <span v-else-if="month[7]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total]]"></column-chart></span>
          <span v-else-if="month[6]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total]]"></column-chart></span>
          <span v-else-if="month[5]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total]]"></column-chart></span>
          <span v-else-if="month[4]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total]]"></column-chart></span>
          <span v-else-if="month[3]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total]]"></column-chart></span>
          <span v-else-if="month[2]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total]]"></column-chart></span>
          <span v-else-if="month[1]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total]]"></column-chart></span>
          <span v-else><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total]]"></column-chart></span>
        </b-col>
      </b-row>
      </b-carousel-slide>


      <b-carousel-slide id='slide_2' img-blank img-alt="Blank image">
        <h3>Today</h3>
        <b-row style='padding-bottom:25px;height: 550px'>
        <b-col md='4' >
          <div>
            <h4>Total Tickets - {{((total[0].total/(total[0].total + total[1].total))*100).toString().slice(0,5)}}% Web</h4>
            <b-table striped hover dark :items="total"></b-table>
          </div>
          <pie-chart  :download="{background: 'white'}" width="auto" height="250px" style='opacity: 0.9;' :data="[[total[0].name, total[0].total], [total[1].name, total[1].total]]" :colors="['#42b983', '#e83e8c']" />
        </b-col>
        <b-col md='8' >
          <div>
            <h5>CA Tickets {{((ca[0].total/(ca[0].total + ca[1].total))*100).toString().slice(0,5)}}% Web</h5>
            <b-table striped hover  dark :items="ca"></b-table>
          </div>
          
          <div>
            <h5>NV Tickets {{((nv[0].total/(nv[0].total + nv[1].total))*100).toString().slice(0,5)}}% Web</h5>
            <b-table striped hover  dark :items="nv"></b-table>
          </div>
        </b-col>
        </b-row>
        
      </b-carousel-slide>

      <b-carousel-slide id='slide_3' img-blank img-alt="Blank image">
        <h3>Today</h3>
        <b-row style='padding-bottom:25px;height: 590px'>
        <b-col lg='4' md='12' >
          <h4>Web Tickets</h4>
          <div v-if="type_csr[1].name != 'HOME'">No Data</div><div v-else>
        <pie-chart :download="{background: 'white'}" width="auto" height="250px" style='opacity: 0.9;'  :data="[[type_web[0].name, type_web[0].total], [type_web[1].name, type_web[1].total],[type_web[2].name, type_web[2].total]]" :colors="['#42b983', '#ffc107', '#e83e8c']" />
        <hr class="my-4" style=" margin-left:175px;margin-right:175px;">
        <h4>DPS Tickets</h4>
        <pie-chart :download="{background: 'white'}" width="auto" height="250px" style='opacity: 0.9;' :data="[[type_csr[0].name, type_csr[0].total], [type_csr[1].name, type_csr[1].total],[type_csr[2].name, type_csr[2].total]]" :colors="['#42b983', '#ffc107', '#e83e8c']" />
        </div>
        </b-col>
        <b-col lg='8' md='12' style="">
          <div><div v-if="type_csr[1].name != 'HOME'">No Data</div><div v-else>
            <h4>Web %</h4>
            <h5 style="margin-bottom: -15px;">
            Contractors: {{((type_web[0].total/(type_web[0].total + type_csr[0].total))*100).toString().slice(0,5)}}% - 
            Homeowners: {{((type_web[1].total/(type_web[1].total + type_csr[1].total))*100).toString().slice(0,5)}}% - 
            Members: {{((type_web[2].total/(type_web[2].total + type_csr[2].total))*100).toString().slice(0,5)}}% </h5>
            <hr class="my-4" style="border-color:#ced4da; margin-left:100px;margin-right:100px;">
            </div>
          </div>
          <div style=" margin-top: -15px">
            <h4>Web Tickets </h4>
            <b-table striped hover dark :items="type_web" ></b-table>
          </div>
        
          <div>
            <h4>DPS Tickets </h4>
            <b-table striped hover dark :items="type_csr"></b-table>
          </div>
        </b-col>
      </b-row>
      </b-carousel-slide>

      <!-- Slides with img slot -->
      <!-- Note the classes .d-block and .img-fluid to prevent browser default image alignment -->
      

    </b-carousel>
  </div>
  <div class="d-lg-none"> 
    <hr class="my-4" style="border-color:#ced4da; margin-left:175px;margin-right:175px;">
<b-row style='padding-bottom:25px;'>
        <b-col lg='4' md='12' >
          <h3>Today</h3>
          <div>
            <h4>total Tickets {{((total[0].total/(total[0].total + total[1].total))*100).toString().slice(0,5)}}% Web</h4>
            <b-table striped hover dark :items="total"></b-table>
          </div>
          <div>
            <h4>CA Tickets {{((ca[0].total/(ca[0].total + ca[1].total))*100).toString().slice(0,5)}}% Web</h4>
            <b-table striped hover dark :items="ca"></b-table>
          </div>
          <div>
            <h4>NV Tickets {{((nv[0].total/(nv[0].total + nv[1].total))*100).toString().slice(0,5)}}% Web</h4>
            <b-table striped hover dark :items="nv"></b-table>
          </div>
        </b-col>
        <hr class="my-4" style="border-color:#ced4da; margin-left:175px;margin-right:175px;">
        <b-col md='12' >
          <div>
            <h3>YTD</h3>
            <h4>{{(ytd[0].total + ytd[1].total).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}} Tickets - {{((ytd[1].total/(ytd[0].total + ytd[1].total))*100).toString().slice(0,5)}}% Web</h4>
            <b-table striped hover dark :items="ytd"></b-table>
          </div>
        </b-col>
        <b-col  md='12'>
          <span v-if="month[12]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total],[month[8].name, month[8].total],[month[9].name, month[9].total],[month[10].name, month[10].total],[month[11].name, month[11].total],[month[12].name, month[12].total]]"></column-chart></span>
          <span v-else-if="month[11]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total],[month[8].name, month[8].total],[month[9].name, month[9].total],[month[10].name, month[10].total],[month[11].name, month[11].total]]"></column-chart></span>
          <span v-else-if="month[10]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total],[month[8].name, month[8].total],[month[9].name, month[9].total],[month[10].name, month[10].total]]"></column-chart></span>
          <span v-else-if="month[9]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total],[month[8].name, month[8].total],[month[9].name, month[9].total]]"></column-chart></span>
          <span v-else-if="month[8]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total],[month[8].name, month[8].total]]"></column-chart></span>
          <span v-else-if="month[7]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total], [month[7].name, month[7].total]]"></column-chart></span>
          <span v-else-if="month[6]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total],[month[6].name, month[6].total]]"></column-chart></span>
          <span v-else-if="month[5]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total],[month[5].name, month[5].total]]"></column-chart></span>
          <span v-else-if="month[4]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total], [month[4].name, month[4].total]]"></column-chart></span>
          <span v-else-if="month[3]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total],[month[3].name, month[3].total]]"></column-chart></span>
          <span v-else-if="month[2]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total],[month[2].name, month[2].total]]"></column-chart></span>
          <span v-else-if="month[1]"><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total], [month[1].name, month[1].total]]"></column-chart></span>
          <span v-else><column-chart :download="{background: 'white'}" height='250px' :data="[[month[0].name, month[0].total]]"></column-chart></span>
        </b-col>
        <hr class="my-4" style="border-color:#ced4da; margin-left:175px;margin-right:175px;">
        <b-col lg='8' md='12' style="position:relative; overflow-y:auto;">
          <h3>User Types</h3>
          <div><div v-if="type_csr[1].name != 'HOME'">No Data</div><div v-else>
            <h4>Web %</h4>
            <h5 style="margin-bottom: -15px;">
            Contractors: {{((type_web[0].total/(type_web[0].total + type_csr[0].total))*100).toString().slice(0,5)}}% - 
            Homeowners: {{((type_web[1].total/(type_web[1].total + type_csr[1].total))*100).toString().slice(0,5)}}% - 
            Members: {{((type_web[2].total/(type_web[2].total + type_csr[2].total))*100).toString().slice(0,5)}}% - </h5>
            <hr class="my-4" style="border-color:#ced4da; margin-left:175px;margin-right:175px;">
            </div>
          </div><div v-if="type_csr[1].name != 'HOME'">No Data</div><div v-else>
          <div style=" margin-top: -15px">
            <h4>Web Tickets by User Type</h4>
            <b-table striped hover dark :items="type_web" ></b-table>
          </div>
        
          <div>
            <h4>DPS Tickets by User Type</h4>
            <b-table striped hover dark :items="type_csr"></b-table>
          </div></div>
          <h4>Web Tickets</h4>
        <pie-chart :download="true" width="auto" height="450px" :data="[[type_web[0].name, type_web[0].total], [type_web[1].name, type_web[1].total],[type_web[2].name, type_web[2].total]]" :colors="['#42b983', '#ffc107', '#e83e8c']" />
        <h4 style='padding-top: 20px'>DPS Tickets</h4>
        <pie-chart :download="true" width="auto" height="450px" :data="[[type_csr[0].name, type_csr[0].total], [type_csr[1].name, type_csr[1].total],[type_csr[2].name, type_csr[2].total]]" :colors="['#42b983', '#ffc107', '#e83e8c']" />
        </b-col>
      </b-row>
      
  </div>
  </div>
    </b-container>
    <b-img src='./src/assets/811-logo.svg' width='115' style="padding-top:30px; padding-bottom: 25px;" />
    
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      total: null,
      dps: null,
      web: null,
      ca: null,
      nv: null,
      type_csr: null,
      type_web: null,
      sat: null,
      month: null,
      months: [],
      ytd: null,
      yesterday: null,
      myDate : new Date().toISOString().slice(5,10)
    }
  },
  mounted () {
    axios.get('https://www.triveea.com/reports/total')
        .then(response => (self.total = response.data.Referral), axios.get('https://www.triveea.com/reports/dps')
        .then(response => (self.dps = response.data.Referral), axios.get('https://www.triveea.com/reports/web')
        .then(response => (self.web = response.data.Referral), axios.get('https://www.triveea.com/reports/ca')
        .then(response => (self.ca = response.data.Referral), axios.get('https://www.triveea.com/reports/nv')
        .then(response => (self.nv = response.data.Referral), axios.get('https://www.triveea.com/reports/type_csr')
        .then(response => (self.type_csr = response.data.Referral), axios.get('https://www.triveea.com/reports/type_web')
        .then(response => (self.type_web = response.data.Referral), axios.get('https://www.triveea.com/reports/sat')
        .then(response => (self.sat = response.data.Referral), axios.get('https://www.triveea.com/reports/month')
        .then(response => (self.month = response.data.Referral), axios.get('https://www.triveea.com/reports/ytd')
        .then(response => (self.ytd = response.data.Referral), axios.get('https://www.triveea.com/reports/yesterday')
        .then(response => (self.yesterday = response.data.Referral))))))))))));
    var self = this;
    setInterval(function(){
      axios.get('https://www.triveea.com/reports/total')
        .then(response => (self.total = response.data.Referral), axios.get('https://www.triveea.com/reports/dps')
        .then(response => (self.dps = response.data.Referral), axios.get('https://www.triveea.com/reports/web')
        .then(response => (self.web = response.data.Referral), axios.get('https://www.triveea.com/reports/ca')
        .then(response => (self.ca = response.data.Referral), axios.get('https://www.triveea.com/reports/nv')
        .then(response => (self.nv = response.data.Referral), axios.get('https://www.triveea.com/reports/type_csr')
        .then(response => (self.type_csr = response.data.Referral), axios.get('https://www.triveea.com/reports/type_web')
        .then(response => (self.type_web = response.data.Referral), axios.get('https://www.triveea.com/reports/sat')
        .then(response => (self.sat = response.data.Referral), axios.get('https://www.triveea.com/reports/month')
        .then(response => (self.month = response.data.Referral), axios.get('https://www.triveea.com/reports/ytd')
        .then(response => (self.ytd = response.data.Referral), axios.get('https://www.triveea.com/reports/yesterday')
        .then(response => (self.yesterday = response.data.Referral))))))))))));
    }, 30000);
      
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f8f9fa;
  margin-top: 30px;
  
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
body {
  background-color:#212529;
}
img {
  max-width: 65%;
    
}
.orientation {
  width: 400px /* normal width */
}
@media print {
  .ortientation {
    width: 100% /* print width */
  }
}
</style>
