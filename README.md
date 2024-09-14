<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Comprehensive Blood Test Results</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.7.0/chart.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/lucide/0.263.1/lucide.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h1, h2 {
            color: #333;
        }
        .chart-container {
            margin-bottom: 30px;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
        }
        .chart-item {
            width: 48%;
            margin-bottom: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }
        th, td {
            padding: 10px;
            border: 1px solid #ddd;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
        .test-group {
            margin-bottom: 40px;
            border: 1px solid #ddd;
            padding: 20px;
            border-radius: 8px;
        }
        .organ-icon {
            width: 24px;
            height: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }
        .result-normal { background-color: #e6ffe6; }
        .result-low { background-color: #ffe6e6; }
        .result-high { background-color: #fff2e6; }
        .test-name {
            display: flex;
            align-items: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Comprehensive Blood Test Results</h1>
        
        <div class="test-group">
            <h2>Comprehensive Metabolic Panel</h2>
            <div class="chart-container" id="cmpCharts">
                <!-- Charts will be added here dynamically -->
            </div>
            <table id="cmpTable">
                <thead>
                    <tr>
                        <th>Test</th>
                        <th>Feb 25, 2022</th>
                        <th>Jun 20, 2022</th>
                        <th>Jan 11, 2023</th>
                        <th>Feb 28, 2023</th>
                        <th>Feb 14, 2024</th>
                        <th>Normal Range</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Data will be populated by JavaScript -->
                </tbody>
            </table>
        </div>

        <div class="test-group">
            <h2>Thyroid Function Tests</h2>
            <div class="chart-container" id="thyroidCharts">
                <!-- Charts will be added here dynamically -->
            </div>
            <table id="thyroidTable">
                <thead>
                    <tr>
                        <th>Test</th>
                        <th>Feb 25, 2022</th>
                        <th>Jun 20, 2022</th>
                        <th>Jan 11, 2023</th>
                        <th>Feb 21, 2023</th>
                        <th>Feb 14, 2024</th>
                        <th>Normal Range</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Data will be populated by JavaScript -->
                </tbody>
            </table>
        </div>

        <div class="test-group">
            <h2>Lipid Panel</h2>
            <div class="chart-container" id="lipidCharts">
                <!-- Charts will be added here dynamically -->
            </div>
            <table id="lipidTable">
                <thead>
                    <tr>
                        <th>Test</th>
                        <th>Aug 26, 2022</th>
                        <th>Jan 11, 2023</th>
                        <th>Feb 28, 2023</th>
                        <th>Feb 14, 2024</th>
                        <th>Normal Range</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Data will be populated by JavaScript -->
                </tbody>
            </table>
        </div>

        <div class="test-group">
            <h2>GFR Calculation</h2>
            <div class="chart-container" id="gfrCharts">
                <!-- Charts will be added here dynamically -->
            </div>
            <table id="gfrTable">
                <thead>
                    <tr>
                        <th>Test</th>
                        <th>Feb 25, 2022</th>
                        <th>Jun 20, 2022</th>
                        <th>Jan 11, 2023</th>
                        <th>Feb 28, 2023</th>
                        <th>Feb 14, 2024</th>
                        <th>Normal Range</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Data will be populated by JavaScript -->
                </tbody>
            </table>
        </div>
    </div>

    <script>
        const testData = {
            cmp: {
                glucose: { values: [76, 106, 93, 96, 99], unit: 'mg/dL', organ: 'Pancreas' },
                creatinine: { values: [0.87, 0.84, 0.90, 0.96, 1.13], unit: 'mg/dL', organ: 'Kidney' },
                bun: { values: [21, 18, 14, 12, 24], unit: 'mg/dL', organ: 'Kidney' },
                sodium: { values: [139, 141, 137, 141, 139], unit: 'mmol/L', organ: 'Kidney' },
                potassium: { values: [3.7, 3.6, 4.3, 4.0, 3.9], unit: 'mmol/L', organ: 'Kidney' },
                chloride: { values: [104, 104, 105, 102, 105], unit: 'mmol/L', organ: 'Kidney' },
                calcium: { values: [9.3, 9.5, 9.5, 10.0, 9.2], unit: 'mg/dL', organ: 'Bone' },
                ast: { values: [25, 19, 19, 19, 23], unit: 'U/L', organ: 'Liver' },
                alt: { values: [19, 14, 13, 15, 15], unit: 'U/L', organ: 'Liver' }
            },
            thyroid: {
                tsh: { values: [1.439, 1.277, 0.880, 1.030, 1.722], unit: 'uIU/mL', organ: 'Thyroid' }
            },
            lipid: {
                cholesterol: { values: [200, 200, 177, 199], unit: 'mg/dL', organ: 'Blood' },
                triglycerides: { values: [54, 62, 72, 118], unit: 'mg/dL', organ: 'Blood' },
                hdlCholesterol: { values: [65, 58, 58, 60], unit: 'mg/dL', organ: 'Blood' },
                ldlCholesterol: { values: [null, 124, 105, 115], unit: 'mg/dL', organ: 'Blood' }
            },
            gfr: {
                gfr: { values: [60, 60, 60, 60, 60], unit: 'mL/min', organ: 'Kidney' }
            },
            normalRanges: {
                glucose: { min: 70, max: 100 },
                creatinine: { min: 0.50, max: 1.20 },
                bun: { min: 5, max: 21 },
                sodium: { min: 135, max: 145 },
                potassium: { min: 3.5, max: 5.5 },
                chloride: { min: 98, max: 110 },
                calcium: { min: 8.5, max: 10.5 },
                ast: { min: 0, max: 34 },
                alt: { min: 0, max: 55 },
                tsh: { min: 0.350, max: 4.94 },
                cholesterol: { min: 100, max: 200 },
                triglycerides: { min: 30, max: 150 },
                hdlCholesterol: { min: 40, max: 125 },
                ldlCholesterol: { min: 0, max: 130 },
                gfr: { min: 60, max: 120 }
            }
        };

        function createChart(containerId, testName, data, normalRange) {
            const chartContainer = document.getElementById(containerId);
            const chartItem = document.createElement('div');
            chartItem.className = 'chart-item';
            const canvas = document.createElement('canvas');
            chartItem.appendChild(canvas);
            chartContainer.appendChild(chartItem);

            const ctx = canvas.getContext('2d');
            return new Chart(ctx, {
                type: 'line',
                data: {
                    labels: Object.keys(testData).find(key => testData[key][testName]) === 'lipid' 
                        ? ['Aug 26, 2022', 'Jan 11, 2023', 'Feb 28, 2023', 'Feb 14, 2024']
                        : ['Feb 25, 2022', 'Jun 20, 2022', 'Jan 11, 2023', 'Feb 28, 2023', 'Feb 14, 2024'],
                    datasets: [{
                        label: `${testName.toUpperCase()} (${data.unit})`,
                        data: data.values,
                        borderColor: 'rgb(75, 192, 192)',
                        tension: 0.1
                    }]
                },
                options: {
                    responsive: true,
                    scales: {
                        y: {
                            beginAtZero: false,
                            min: normalRange.min,
                            max: normalRange.max
                        }
                    },
                    plugins: {
                        title: {
                            display: true,
                            text: `${testName.toUpperCase()} (${data.unit})`
                        }
                    }
                }
            });
        }

        function getOrganIcon(organ) {
            const iconMap = {
                'Kidney': 'activity',
                'Liver': 'activity',
                'Pancreas': 'candy',
                'Thyroid': 'triangle',
                'Blood': 'droplets',
                'Bone': 'bone'
            };
            return `<i data-lucide="${iconMap[organ] || 'activity'}" class="organ-icon"></i>`;
        }

        function getResultClass(value, min, max) {
            if (value === null) return '';
            if (value < min) return 'result-low';
            if (value > max) return 'result-high';
            return 'result-normal';
        }

        function populateTable(tableId, data, normalRanges) {
            const table = document.getElementById(tableId);
            const tbody = table.querySelector('tbody');
            tbody.innerHTML = '';
            Object.entries(data).forEach(([test, testData]) => {
                const row = tbody.insertRow();
                const testNameCell = row.insertCell();
                testNameCell.innerHTML = `<div class="test-name">${getOrganIcon(testData.organ)}${test.toUpperCase()} (${testData.unit})</div>`;
                testData.values.forEach((value, index) => {
                    const cell = row.insertCell();
                    cell.textContent = value !== null ? value : 'N/A';
                    cell.className = getResultClass(value, normalRanges[test].min, normalRanges[test].max);
                });
                const rangeCell = row.insertCell();
                rangeCell.textContent = `${normalRanges[test].min} - ${normalRanges[test].max}`;
            });
        }

        // Create charts and populate tables
        Object.entries(testData).forEach(([group, tests]) => {
            if (group !== 'normalRanges') {
                Object.entries(tests).forEach(([test, data]) => {
                    createChart(`${group}Charts`, test, data, testData.normalRanges[test]);
                });
                populateTable(`${group}Table`, tests, testData.normalRanges);
            }
        });

        // Initialize Lucide icons
        lucide.createIcons();
    </script>
</body>
</html>
