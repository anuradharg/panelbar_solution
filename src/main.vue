<template>
<div>
        <div class="col-md-12">
            <div class=" mt-3">
                <button class="btn-primary" @click="addConfigurableSection()">+ Configurable Section</button>
            </div>
        </div>
        <div>
<div :key="forceRender">
  <kendo-panelbar ref="panelbar" id="panelbar">
        <li v-bind:key="idx" v-for="(item, idx) in groupHeaders">
            {{item.name}}
                <ul>
                <div v-bind:key="i" v-for="(itemSection, i) in groupHeaders"
                    style="background: #fff;">
                    <li class="p-2 col-md-12">
                        <div class="row">
                            <div class="col-md-2">
                               <label>Test {{i}} </label>
                            </div>
                            <div class="col-md-5" >
                                <textarea />
                            </div>                            
                            <div class="col-md-5">
                                <textarea  />
                            </div>
                        </div>
                    </li>
                </div>

                <li class="subsections" v-bind:key="index" v-for="(subitem, index) in item.subsections">
                    <span class="k-icon k-i-arrow-60-right"></span>&nbsp;{{subitem.name}}
                    <div class="content p-2">
                        <div class="p-1" v-bind:key="index"
                            v-for="(itemSection, index) in groupHeaders">
                            <div class="row">
                                <div class="col-md-2">
                                    <label>Test {{index}} </label>
                                </div>
                                <div class="col-md-5">
                                    <textarea  />
                                </div>
                                <div class="col-md-5">
                                    <textarea  />
                                </div>
                            </div>
                        </div>
                    </div>
                </li>
            </ul>
        </li>
    </kendo-panelbar>
    </div>

</div>
</div>
</template>
<script>
import { PanelBar } from '@progress/kendo-layout-vue-wrapper';
export default {
  components: {
    'kendo-panelbar': PanelBar
  },
  computed:{
      forceRender: function(){
          return this.reRender;
      }
  },
   data: function() {
        return {
            reRender:1,
            ConfigurableSectionCount:3,
            groupHeaders: [
                {
                    name: "Section 1",
                    subsections: [
                        {
                            name: "Subsection 1"
                        },
                        {
                            name: "Subsection 2"
                        },
                        {
                            name: "Subsection 3"
                        },
                    ]
                },
                {
                    name: "Section 2"
                },
                {
                    name: "Configurable Section 1"
                },
                {
                    name: "Configurable Section 2"
                },
                {
                    name: "Configurable Section 3"
                },
                {
                    name: "Section 3"
                },
                {
                    name: "Section 4"
                },
                {
                    name: "Section 5"
                }
            ]
        }   
        },
         methods: {
              addConfigurableSection: function(e){
                let csCount = this.ConfigurableSectionCount + 1;
                let configurableSectionHeader= {
                        name: "Configurable Section " + csCount
                    }             
                let grpHeaders = JSON.parse(JSON.stringify(this.groupHeaders));

                const mainSection = "Section 3"
                let index = -1;
                 grpHeaders.find(function(item, i){
                    if(item.name === mainSection){
                        index = i;
                    }
                });
                grpHeaders.splice(index, 0,configurableSectionHeader);

                this.groupHeaders=[];
                this.groupHeaders=grpHeaders;
                this.ConfigurableSectionCount = csCount;
                this.reRender+=1;
            },
            
            getSections: function (GroupHeaderName) {
                           
            },
            getSubSections: function (GroupHeaderName) {
            },
         }
    }
</script>
<style>
    #panelbar .k-sprite {
        background-image: url("https://demos.telerik.com/kendo-ui/content/web/treeview/coloricons-sprite.png");
    }

    .rootfolder { background-position: 0 0; }
    .folder     { background-position: 0 -16px; }
    .pdf        { background-position: 0 -32px; }
    .html       { background-position: 0 -48px; }
    .image      { background-position: 0 -64px; }
</style>
