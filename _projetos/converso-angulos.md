---
layout: page
title: Conversor de Ângulos
descricao: Calculadora de apoio a para converter ângulos
imagem: https://i.ytimg.com/vi/4dWGhmL2FKs/hq720.jpg?sqp=-oaymwEhCK4FEIIDSFryq4qpAxMIARUAAAAAGAElAADIQj0AgKJD&rs=AOn4CLBGaDaT5AtX9ATo3Y1atQBQr4oZ6w
order: 2
sidebar:
    nav: false
---

<style>
/* Esconde a barra lateral direita apenas nesta página */
/* Apenas para a página nivelamento trigonométrico */
#panel-wrapper {
  display: none !important;
}

.col-xl-9 {
  flex: 0 0 100% !important;
  max-width: 100% !important;
}

.row {
  margin-right: 0 !important;
  margin-left: 0 !important;
}
.container {
  max-width: 100% !important;
  width: 100% !important;
  padding-left: 2rem;
  padding-right: 2rem;
}



</style>

<!-- Conteúdo principal -->
<main class="col-md-9 col-lg-10 p-4 bg-white">
<h2 class="mb-4">Conversor de Ângulos</h2>

<div class="row mb-3">
<div class="col-md-6 col-lg-4">
<label for="angleValue" class="form-label">Valor do Ângulo</label>
<input type="number" class="form-control" id="angleValue" placeholder="Insira um valor...">
</div>
<div class="col-md-6 col-lg-4">
<label for="angleUnit" class="form-label">Unidade</label>
<select class="form-select" id="angleUnit">
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

<script src="{{ '/assets/js/niv_trig_reciprocas.js' | relative_url }}"></script>
<script src="{{ '/assets/js/niv_trig_simples.js' | relative_url }}"></script>
<script src="{{ '/assets/js/niv_trig_tabela.js' | relative_url }}"></script>
<!-- Bootstrap CSS -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-VzCcJ1HZt1YhFjHbKLDItuXQbZ05ks+1N+E0rA5qJ0xQz08N2DD1l91X5nUJZxkz" crossorigin="anonymous">

<!-- Bootstrap JS Bundle (inclui Popper.js, necessário para abas, dropdowns, etc.) -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"></script>
