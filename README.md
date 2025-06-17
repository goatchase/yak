<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Home Run Predictor</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet"/>
  <style>
    body {
      font-family: 'Roboto', sans-serif;
      background: #f5f5f5;
      padding: 20px;
    }

    h1 {
      text-align: center;
      margin-bottom: 20px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      background: white;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      border-radius: 10px;
      overflow: hidden;
    }

    thead {
      background-color: #333;
      color: white;
    }

    th, td {
      padding: 10px;
      text-align: center;
      border-bottom: 1px solid #ddd;
    }

    tr:hover {
      background-color: #f1f1f1;
    }

    th {
      cursor: pointer;
    }

    .highlight {
      background-color: #e6ffe6;
    }
  </style>
</head>
<body>

  <h1>Home Run Predictor Table</h1>

  <table id="hrPredictorTable">
    <thead>
      <tr>
        <th onclick="sortTable(0)">Batter</th>
        <th onclick="sortTable(1)">Team</th>
        <th onclick="sortTable(2)">Opponent</th>
        <th onclick="sortTable(3)">Pitcher</th>
        <th onclick="sortTable(4)">Ballpark</th>
        <th onclick="sortTable(5)">Temp (°F)</th>
        <th onclick="sortTable(6)">Wind (MPH / Dir)</th>
        <th onclick="sortTable(7)">Humidity (%)</th>
        <th onclick="sortTable(8)">HR/PA vs Hand</th>
        <th onclick="sortTable(9)">P HR/PA vs Hand</th>
        <th onclick="sortTable(10)">PA Since HR</th>
      </tr>
    </thead>
    <tbody>
      <!-- Example Row -->
      <tr>
        <td>Aaron Judge</td>
        <td>NYY</td>
        <td>BOS</td>
        <td>Chris Sale (LHP)</td>
        <td>Yankee Stadium</td>
        <td>78</td>
        <td>10 / Out</td>
        <td>65</td>
        <td>0.085</td>
        <td>0.065</td>
        <td>18</td>
      </tr>
      <tr class="highlight">
        <td>Kyle Schwarber</td>
        <td>PHI</td>
        <td>NYM</td>
        <td>Jose Quintana (LHP)</td>
        <td>Citizens Bank Park</td>
        <td>85</td>
        <td>12 / In</td>
        <td>70</td>
        <td>0.091</td>
        <td>0.077</td>
        <td>27</td>
      </tr>
      <tr>
        <td>Matt Olson</td>
        <td>ATL</td>
        <td>MIA</td>
        <td>Edward Cabrera (RHP)</td>
        <td>Truist Park</td>
        <td>82</td>
        <td>8 / Out</td>
        <td>55</td>
        <td>0.080</td>
        <td>0.071</td>
        <td>7</td>
      </tr>
    </tbody>
  </table>

  <script>
    function sortTable(n) {
      const table = document.getElementById("hrPredictorTable");
      let switching = true;
      let dir = "asc";
      let switchcount = 0;

      while (switching) {
        switching = false;
        const rows = table.rows;

        for (let i = 1; i < rows.length - 1; i++) {
          let shouldSwitch = false;
          const x = rows[i].getElementsByTagName("TD")[n];
          const y = rows[i + 1].getElementsByTagName("TD")[n];

          let xContent = isNaN(parseFloat(x.innerHTML)) ? x.innerHTML.toLowerCase() : parseFloat(x.innerHTML);
          let yContent = isNaN(parseFloat(y.innerHTML)) ? y.innerHTML.toLowerCase() : parseFloat(y.innerHTML);

          if ((dir === "asc" && xContent > yContent) ||
              (dir === "desc" && xContent < yContent)) {
            shouldSwitch = true;
            break;
          }
        }

        if (shouldSwitch) {
          rows[i].parentNode.insertBefore(rows[i + 1], rows[i]);
          switching = true;
          switchcount++;
        } else {
          if (switchcount === 0 && dir === "asc") {
            dir = "desc";
            switching = true;
          }
        }
      }
    }
  </script>

</body>
</html>
