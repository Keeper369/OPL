<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Spare Parts Order List</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  html, body { width: 100%; min-height: 100vh; font-family: Arial, sans-serif; font-size: 14px; background: #fff; }
  .page { width: 100%; min-height: 100vh; padding: 30px 40px; }

.top-bar { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; }
.top-bar h1 { font-size: 20px; font-weight: bold; text-transform: uppercase; }

.save-btn {
background: #222; color: #fff; border: none;
padding: 9px 22px; cursor: pointer; font-size: 13px; font-family: Arial, sans-serif;
}
.save-btn:hover { background: #444; }

/* Buyer info */
.buyer-row { margin-bottom: 16px; font-size: 14px; }
.buyer-row strong { margin-right: 8px; }

table { width: 100%; border-collapse: collapse; margin-bottom: 16px; }
thead tr { background: #222; color: #fff; }
thead th { padding: 10px 12px; text-align: center; font-size: 13px; font-weight: bold; border: 1px solid #444; white-space: nowrap; }
tbody td { padding: 10px 12px; border: 1px solid #ccc; vertical-align: middle; text-align: center; }
tbody td.left { text-align: left; }
tbody tr:nth-child(even) { background: #f9f9f9; }
[contenteditable]:focus { outline: 2px solid #0078d4; background: #fff; }

.pic-wrap {
width: 80px; height: 70px; border: 1.5px dashed #aaa;
display: flex; flex-direction: column; align-items: center; justify-content: center;
cursor: pointer; margin: 0 auto; position: relative; overflow: hidden; background: #fafafa;
}
.pic-wrap:hover { border-color: #0078d4; background: #f0f7ff; }
.pic-wrap input[type=“file”] { position: absolute; inset: 0; opacity: 0; cursor: pointer; width: 100%; height: 100%; }
.pic-wrap .icon { font-size: 18px; color: #aaa; pointer-events: none; }
.pic-wrap .lbl { font-size: 9px; color: #bbb; pointer-events: none; margin-top: 2px; }
.pic-wrap img { position: absolute; inset: 0; width: 100%; height: 100%; object-fit: cover; }

.add-btn { background: #222; color: #fff; border: none; padding: 8px 20px; cursor: pointer; font-size: 13px; margin-bottom: 24px; font-family: Arial, sans-serif; }
.add-btn:hover { background: #444; }

.footer { border-top: 2px solid #000; padding-top: 16px; display: flex; justify-content: space-between; align-items: flex-end; flex-wrap: wrap; gap: 20px; }
.footer .notes { font-size: 12px; color: #555; max-width: 500px; line-height: 1.7; }
.sig-line { border-top: 1px solid #000; width: 200px; padding-top: 6px; font-size: 12px; color: #444; text-align: center; margin-top: 40px; }

@media print {
.add-btn, .save-btn { display: none !important; }
.pic-wrap input[type=“file”] { display: none; }
}
</style>

</head>
<body>
<div class="page">

  <div class="top-bar">
    <h1>Spare Parts Order List</h1>
    <button class="save-btn" onclick="window.print()">💾 Save as PDF</button>
  </div>

  <div class="buyer-row">
    <strong>Buyer:</strong> Sok Ngoun
  </div>

  <table id="order-table">
    <thead>
      <tr>
        <th style="width:50px;">No.</th>
        <th>Product Name</th>
        <th>Model / Specification</th>
        <th>Part Number</th>
        <th style="width:100px;">Picture</th>
        <th style="width:110px;">Quantity</th>
      </tr>
    </thead>
    <tbody id="tbody">
      <tr>
        <td>1</td>
        <td class="left" contenteditable="true">PUMP, CAB Tilt</td>
        <td contenteditable="true">KOREA</td>
        <td contenteditable="true">643907A032</td>
        <td>
          <div class="pic-wrap">
            <input type="file" accept="image/*" onchange="previewImg(this)">
            <div class="icon">📷</div><div class="lbl">Upload</div>
          </div>
        </td>
        <td contenteditable="true">20 PCS</td>
      </tr>
      <tr>
        <td>2</td>
        <td class="left" contenteditable="true">Click to edit</td>
        <td contenteditable="true">—</td>
        <td contenteditable="true">—</td>
        <td>
          <div class="pic-wrap">
            <input type="file" accept="image/*" onchange="previewImg(this)">
            <div class="icon">📷</div><div class="lbl">Upload</div>
          </div>
        </td>
        <td contenteditable="true">— PCS</td>
      </tr>
      <tr>
        <td>3</td>
        <td class="left" contenteditable="true">Click to edit</td>
        <td contenteditable="true">—</td>
        <td contenteditable="true">—</td>
        <td>
          <div class="pic-wrap">
            <input type="file" accept="image/*" onchange="previewImg(this)">
            <div class="icon">📷</div><div class="lbl">Upload</div>
          </div>
        </td>
        <td contenteditable="true">— PCS</td>
      </tr>
    </tbody>
  </table>

<button class="add-btn" onclick="addRow()">+ Add Row</button>

  <div class="footer">
    <div class="notes">
      <strong>Notes:</strong><br>
      All goods subject to inspection upon delivery.<br>
      Payment and delivery terms as per agreement.<br>
      This order is valid with authorized signature.
    </div>
    <div>
      <div class="sig-line">Sok Ngoun — Buyer</div>
    </div>
  </div>

</div>

<script>
  function previewImg(input) {
    const wrap = input.parentElement;
    const old = wrap.querySelector('img');
    if (old) old.remove();
    if (input.files && input.files[0]) {
      const reader = new FileReader();
      reader.onload = e => {
        const img = document.createElement('img');
        img.src = e.target.result;
        wrap.appendChild(img);
        wrap.querySelector('.icon').style.display = 'none';
        wrap.querySelector('.lbl').style.display = 'none';
      };
      reader.readAsDataURL(input.files[0]);
    }
  }

  let count = 3;
  function addRow() {
    count++;
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${count}</td>
      <td class="left" contenteditable="true">Click to edit</td>
      <td contenteditable="true">—</td>
      <td contenteditable="true">—</td>
      <td>
        <div class="pic-wrap">
          <input type="file" accept="image/*" onchange="previewImg(this)">
          <div class="icon">📷</div><div class="lbl">Upload</div>
        </div>
      </td>
      <td contenteditable="true">— PCS</td>
    `;
    document.getElementById('tbody').appendChild(tr);
  }
</script>

</body>
</html>