<template>
  <div id="app">
    <div @click="generatePDF()" class="np-btn">Generate PDF</div>

    <vue-html2pdf
      :show-layout="false"
      :float-layout="true"
      :enable-download="true"
      :preview-modal="true"
      :paginate-elements-by-height="1400"
      filename="nightprogrammerpdf"
      :pdf-quality="2"
      :manual-pagination="false"
      pdf-format="a4"
      :pdf-margin="10"
      pdf-orientation="portrait"
      pdf-content-width="800px"
      @progress="onProgress($event)"
      ref="html2Pdf"
    >
      <section slot="pdf-content">
        <ContentToPrint />
      </section>
    </vue-html2pdf>
    <div>
      <ContentToPrint />
    </div>
  </div>
</template>

<script>
import VueHtml2pdf from "vue-html2pdf";
import ContentToPrint from "./ContentToPrint";

export default {
  name: "App",
  methods: {
    onProgress(event) {
      console.log(`Processed: ${event} / 100`);
    },
    hasGenerated() {
      alert("PDF generated successfully!");
    },
    generatePDF() {
      this.$refs.html2Pdf.generatePdf();
    },
  },
  components: {
    VueHtml2pdf,
    ContentToPrint,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.np-btn {
  padding: 2px 8px;
  margin: 12px 8px;
  border: 1px solid #da1010;
  width: 110px;
  background: #da1010;
  border-radius: 6px;
  color: #ffffff;
  cursor: pointer;
}
</style>
