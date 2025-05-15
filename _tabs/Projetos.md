---
layout: page
title: Projetos
icon: fas fa-archive
order: 1
---

<div class="container mt-4">

<!-- Head -->
<link rel="stylesheet" href="/assets/css/bootstrap.min.css">

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

<script src="/assets/js/bootstrap.bundle.min.js"></script>
