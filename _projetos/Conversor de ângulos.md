---
layout: page
title: Conversor de ângulos
icon: fas fa-archive
imagem: "https://files.passeidireto.com/7f4a1ff3-1a63-4d18-9d8b-e875f326d8f0/bg2.png"
---

<!-- Head -->
<link rel="stylesheet" href="/assets/css/bootstrap.min.css">

<main class="col-md-9 col-lg-10 p-4 bg-white">
<h2 class="mb-4">Conversor de Ângulos</h2>

<div class="row mb-3">
<div class="col-md-6 col-lg-4">
<label for="angleValue" class="form-label">Valor do Ângulo</label>
<input type="number" class="form-control" id="angleValue" placeholder="Insira um valor...">
</div>
<div class="col-md-6 col-lg-4">
<label for="angleUnit" class="form-label">Unidade</label>
<select class="form-select border-primary rounded shadow" id="angleUnit">
<option value="deg">Graus (°)</option>
<option value="deghms">Graus (hh:mm:ss)</option>
<option value="rad">Radianos (rad)</option>
<option value="gon">Gradianos (grad)</option>
</select>
</div>
</div>

<h5 class="mt-4">Conversões:</h5>
<ul class="list-group" id="conversionResults">
<li class="list-group-item"><strong>Graus:</strong> <span id="outDeg">-</span> °</li>
<li class="list-group-item"><strong>Graus (hh:mm:ss):</strong> <span id="outDeghms">-</span></li>
<li class="list-group-item"><strong>Radianos:</strong> <span id="outRad">-</span> rad</li>
<li class="list-group-item"><strong>Gradianos:</strong> <span id="outGon">-</span> grad</li>
</ul>
</main>

<script>
function toRadians(deg) {
return deg * (Math.PI / 180);
}

function toGradians(deg) {
return deg * (10 / 9);
}

function fromRadians(rad) {
return rad * (180 / Math.PI);
}

function fromGradians(gon) {
return gon * (9 / 10);
}

function degToDMS(deg) {
const d = Math.floor(deg);
const minFloat = (deg - d) * 60;
const m = Math.floor(minFloat);
const s = ((minFloat - m) * 60).toFixed(2);
return `${d}° ${m}' ${s}"`;
}

function DMSToDeg(hmsStr) {
const parts = hmsStr.trim().split(/[:\s°'"]+/).filter(Boolean).map(Number);
const [h, m = 0, s = 0] = parts;
if (isNaN(h)) throw "Invalid DMS input";
return h + (m / 60) + (s / 3600);
}

function updateConversions() {
const input = document.getElementById('angleValue').value;
const unit = document.getElementById('angleUnit').value;

let degrees;

if (unit === 'deghms') {
try {
degrees = DMSToDeg(input);
} catch {
degrees = NaN;
}
} else {
degrees = parseFloat(input);
if (unit === 'rad') degrees = fromRadians(degrees);
if (unit === 'gon') degrees = fromGradians(degrees);
}

if (isNaN(degrees)) {
document.getElementById('outDeg').textContent = '-';
document.getElementById('outDeghms').textContent = '-';
document.getElementById('outRad').textContent = '-';
document.getElementById('outGon').textContent = '-';
return;
}

document.getElementById('outDeg').textContent = degrees.toFixed(6);
document.getElementById('outDeghms').textContent = degToDMS(degrees);
document.getElementById('outRad').textContent = toRadians(degrees).toFixed(6);
document.getElementById('outGon').textContent = toGradians(degrees).toFixed(6);
}

document.getElementById('angleValue').addEventListener('input', updateConversions);
document.getElementById('angleUnit').addEventListener('change', () => {
const unit = document.getElementById('angleUnit').value;
const input = document.getElementById('angleValue');
input.type = (unit === 'deghms') ? 'text' : 'number';
input.placeholder = (unit === 'deghms') ? 'Ex: 45 30 15' : 'Insira um valor...';
updateConversions();
});
</script>

<!-- No fim do body -->
<script src="/assets/js/bootstrap.bundle.min.js"></script>
