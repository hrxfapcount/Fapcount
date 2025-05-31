<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>NoFap Streak Tracker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #111;
      color: #fff;
      margin: 0;
      padding: 2rem;
    }
    h1 {
      text-align: center;
      color: #0f0;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 2rem;
    }
    th, td {
      padding: 1rem;
      border: 1px solid #444;
      text-align: center;
    }
    button {
      padding: 0.5rem 1rem;
      margin: 0.2rem;
      border: none;
      cursor: pointer;
    }
    .clean {
      background: #2ecc71;
    }
    .relapse {
      background: #e74c3c;
    }
    input, textarea {
      background: #222;
      border: 1px solid #555;
      color: white;
      padding: 0.5rem;
      width: 90%;
    }
  </style>
</head>
<body>
  <h1>NoFap Streak Tracker</h1>
  <table id="tracker">
    <tr>
      <th>Day</th>
      <th>Date</th>
      <th>Clean?</th>
      <th>Trigger</th>
      <th>Notes</th>
    </tr>
  </table>  <script>
    const table = document.getElementById('tracker');
    const days = 30;

    function saveData(day, key, value) {
      localStorage.setItem(`day${day}_${key}`, value);
    }

    function getData(day, key) {
      return localStorage.getItem(`day${day}_${key}`) || '';
    }

    for (let i = 1; i <= days; i++) {
      const date = new Date();
      date.setDate(date.getDate() + i - 1);
      const dateStr = date.toISOString().split('T')[0];

      const row = table.insertRow();
      row.insertCell(0).innerText = i;
      row.insertCell(1).innerText = dateStr;

      const statusCell = row.insertCell(2);
      const triggerCell = row.insertCell(3);
      const notesCell = row.insertCell(4);

      const cleanBtn = document.createElement('button');
      cleanBtn.textContent = '✅';
      cleanBtn.className = 'clean';
      cleanBtn.onclick = () => {
        saveData(i, 'status', '✅');
        statusCell.innerText = '✅';
      };

      const relapseBtn = document.createElement('button');
      relapseBtn.textContent = '❌';
      relapseBtn.className = 'relapse';
      relapseBtn.onclick = () => {
        saveData(i, 'status', '❌');
        statusCell.innerText = '❌';
      };

      statusCell.appendChild(cleanBtn);
      statusCell.appendChild(relapseBtn);

      const triggerInput = document.createElement('input');
      triggerInput.value = getData(i, 'trigger');
      triggerInput.onchange = () => saveData(i, 'trigger', triggerInput.value);
      triggerCell.appendChild(triggerInput);

      const notesInput = document.createElement('textarea');
      notesInput.rows = 2;
      notesInput.value = getData(i, 'notes');
      notesInput.onchange = () => saveData(i, 'notes', notesInput.value);
      notesCell.appendChild(notesInput);

      // Load saved status
      const savedStatus = getData(i, 'status');
      if (savedStatus) statusCell.innerText = savedStatus;
    }
  </script></body>
</html
