# matran <script>
    function createMatrixInputs() {
      const m = parseInt(document.getElementById("rowsA").value);
      const n = parseInt(document.getElementById("colsA").value);
      const p = parseInt(document.getElementById("rowsB").value);
      const q = parseInt(document.getElementById("colsB").value);

      const container = document.getElementById("matrixInputs");
      const result = document.getElementById("result");
      container.innerHTML = "";
      result.innerHTML = "";

      if (isNaN(m) || isNaN(n) || isNaN(p) || isNaN(q)) {
        container.innerHTML = "<p>⚠️ Vui lòng nhập đầy đủ kích thước.</p>";
        return;
      }

      if (n !== p) {
        container.innerHTML = "<p>❌ Không thể nhân: số cột của A phải bằng số hàng của B.</p>";
        return;
      }

      const tableA = generateMatrixTable("A", m, n);
      const tableB = generateMatrixTable("B", p, q);

      container.innerHTML += "<h3>Nhập ma trận A:</h3>" + tableA;
      container.innerHTML += "<h3>Nhập ma trận B:</h3>" + tableB;
      container.innerHTML += `<button onclick="multiplyMatrices(${m}, ${n}, ${q})">Nhân ma trận</button>`;
    }

    function generateMatrixTable(id, rows, cols) {
      let html = `<table border="1" class="matrix">`;
      for (let i = 0; i < rows; i++) {
        html += "<tr>";
        for (let j = 0; j < cols; j++) {
          html += `<td><input type="number" id="${id}_${i}_${j}" /></td>`;
        }
        html += "</tr>";
      }
      html += "</table>";
      return html;
    }

    function multiplyMatrices(m, n, q) {
      const A = [];
      const B = [];

      for (let i = 0; i < m; i++) {
        A[i] = [];
        for (let j = 0; j < n; j++) {
          A[i][j] = parseFloat(document.getElementById(`A_${i}_${j}`).value) || 0;
        }
      }

      for (let i = 0; i < n; i++) {
        B[i] = [];
        for (let j = 0; j < q; j++) {
          B[i][j] = parseFloat(document.getElementById(`B_${i}_${j}`).value) || 0;
        }
      }

      const C = [];
      for (let i = 0; i < m; i++) {
        C[i] = [];
        for (let j = 0; j < q; j++) {
          let sum = 0;
          for (let k = 0; k < n; k++) {
            sum += A[i][k] * B[k][j];
          }
          C[i][j] = sum;
        }
      }

      displayResult(C);
    }

    function displayResult(matrix) {
      let html = "<h3>Kết quả ma trận C = A × B:</h3><table border='1' class='matrix'>";
      for (let i = 0; i < matrix.length; i++) {
        html += "<tr>";
        for (let j = 0; j < matrix[0].length; j++) {
          html += `<td>${matrix[i][j]}</td>`;
        }
        html += "</tr>";
      }
      html += "</table>";
      document.getElementById("result").innerHTML = html;
    }
  </script>

</body>
</html>
