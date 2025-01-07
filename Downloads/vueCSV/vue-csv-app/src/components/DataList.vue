<template>
  <div>
    <h1>Data List</h1>
    <table>
      <tr>
        <th>Asset Name</th>
        <th>Department</th>
      </tr>
      <tr v-for="item in data" :key="item.asset">
        <td>{{ item.asset }}</td>
        <td>{{ item.department }}</td>
      </tr>
    </table>
    <button @click="downloadCSV">Download CSV</button>
  </div>
</template>

<script>

export default {
  data() {
    return {
      data: [
        { asset: "Printer", department: "HR" },
        { asset: "Monitor", department: "IT" },
        { asset: "Barcode Scanner", department: "ACCOUNT" }
      ]
    }
  },
  methods: {
  downloadCSV() {
    let csvContent = `Asset Name,Department\n`;
    
    this.data.forEach(item => {
      csvContent += `${item.asset},${item.department}\n`;
    });

    // Create a Blob object from the CSV string
    const blob = new Blob([csvContent], {type: 'text/csv;charset=utf-8;'});

    // Create a URL for the Blob
    const url = window.URL.createObjectURL(blob);

    // Create a temporary anchor element
    const link = document.createElement('a');

    // Set the href attribute to the Blob URL
    link.href = url;

    // Set the download attribute to specify the filename
    link.download = 'asset_department_list.csv';

    // Append the anchor element to the document
    document.body.appendChild(link);

    // Simulate a click on the anchor element
    link.click();

    // Remove the anchor element after downloading
    document.body.removeChild(link);
  }
}
}
</script>
