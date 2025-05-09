---
layout: page
title: Projetos
icon: fas fa-archive
order: 1
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

<div class="container mt-4">

<!-- Campo de Pesquisa -->
<div class="mb-4">
<input type="text" class="form-control" id="searchProjetos" placeholder="Pesquisar projetos..." onkeyup="filtrarProjetos()">
</div>

<div class="row row-cols-1 row-cols-md-3 g-4" id="gridProjetos">
{% assign projetos_ordenados = site.projetos | sort: "order" %}
{% for projeto in projetos_ordenados %}
<div class="col projeto-card"
data-title="{{ projeto.title | downcase }}"
data-descricao="{{ projeto.descricao | downcase }}">
<div class="card adapt-dark h-100 d-flex flex-column" style="width: 100%;">
<img src="{{ projeto.imagem }}" class="card-img-top" alt="Imagem do projeto {{ projeto.title }}">
<div class="card-body d-flex flex-column">
<h5 class="card-title">{{ projeto.title }}</h5>
<p class="card-text flex-grow-1">{{ projeto.descricao }}</p>
<a href="{{ projeto.url }}" class="btn btn-primary mt-auto w-100">Entrar</a>
</div>
</div>
</div>
{% endfor %}
</div>


<!-- Script de pesquisa -->
<script>
function removerAcentos(texto) {
return texto
  .normalize("NFD")
  .replace(/[\u0300-\u036f]/g, "")
  .toLowerCase();
}

function filtrarProjetos() {
const input = removerAcentos(document.getElementById("searchProjetos").value);
const cards = document.querySelectorAll(".projeto-card");

cards.forEach(card => {
  const title = removerAcentos(card.getAttribute("data-title") || "");
  const descricao = removerAcentos(card.getAttribute("data-descricao") || "");
  const textoCompleto = title + " " + descricao;

  if (textoCompleto.includes(input)) {
    card.style.display = "block"; // ou "flex" se necessário
  } else {
    card.style.display = "none";
  }
});
}
</script>

