+++
date = '2025-09-05T10:55:55+01:00'
draft = false
title = 'Criar Um Blog Com Hugo'
description = ''
author = 'Damião'
tags = ['blog','hugo']
image = 'https://tiiny.host/blog/assets/images/hugo-logo-wide.svg'
+++


Uma das coisas que sempre quis fazer, mas sempre coloquei entraves foi criar um site, mais especificamente um blog! 

Depois de começar a minha jornada em desenvolvimento comecei a ficar sem desculpa para o fazer, mas depois veio a questão e como o faço? Que funcionalidades quero? Uso wordpress ou faço algo de raiz? Isto originou uma pesquisa até encontrar o vídeo do [Fireship.io](https://www.youtube.com/@Fireship) a falar do Hugo.

{{< youtube id="0RKpf3rK57I" >}}


## O que é o Hugo?

[Hugo](https://gohugo.io/) é um Open-Source SSG (Static Site Generator) feito em [Go](https://go.dev/), que é conhecido pelo seu performace. Existem vários [themes](https://themes.gohugo.io/themes) para começar imediatamente, mas também é possível criar os nosso próprios templates!

O que mais me suscitou interesse foi a simplicidade de criar posts em Markdown que o Hugo faz render para páginas HTML.

## Instalar Hugo

Para instalar, visto que estou numa Windows Machine, usei o [Choco](https://community.chocolatey.org/) com:

```powershell
choco install hugo-extended
```

Para outros sistemas operativos, por favor ler a documentação do Hugo.

### Criar um site Hugo

Depois de instalado, basta criar um novo diretório vazio e correr os comandos abaixo.

```bash
mkdir blog
cd blog
hugo new site damiaodoesdev
git init 
```

Com isto foi criado um novo site Hugo.

Agora precisamos de instalar um tema, para este exemplo vou usar o [PaperMod](https://github.com/adityatelange/hugo-PaperMod).

```bash
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod themes/papermod
echo theme='papermod' >> hugo.toml
hugo server
```

E pronto temos um blog criado… 

Agora vamos mudar algumas configurações como o nome do autor, a descrição, o nome do site.

Recomendo ler a documentação do [PaperMod](https://github.com/adityatelange/hugo-PaperMod?tab=readme-ov-file) para entender o que se está a fazer.

Para editar o nome do site vamos fazer o seguinte:

```bash
echo title = '<Nome do site>' >> hugo.toml
echo [params] >> hugo.toml
echo author = '<O nome do autor>' >> hugo.toml
echo ShowPostNav = 'true'>> hugo.toml
```

E neste momento é suposto ter algo assim:

![Site_Hugo.png](/images/criar-um-blog-em-hugo/Site_Hugo.png)

Isto parece muito vazio… vamos então adicionar conteúdo à página inicial criando na pasta /content um ficheiro _index.md (para um exemplo podemos consultar a o _index.md na pasta do theme)

```markdown
# Olá este é o meu site em Hugo
Aqui vou mostrar como se faz um site com Hugo
```

Agora se voltarmos à página vemos as alterações que fizemos!

![image.png](/images/criar-um-blog-em-hugo/Index.png)

E pronto temos um site 😀

## Adicionar o primeiro Post!

Agora tudo o que nos falta é adicionar conteúdo ao nosso blog e para isso escrever o seguinte comando hugo:

```powershell
hugo new content posts/<nome-do-post>.md
```

Depois vamos ao documento e começamos a escrever o post:

```powershell
+++
date = '2025-09-05T12:48:39+01:00'
draft = false
title = 'Primeiro Post'
+++
Este é o meu primeiro post no blog em Hugo.
```

E pronto, agora sim temos um blog com posts 😀

![image.png](/images/criar-um-blog-em-hugo/Primeiro_Post.png)

De qualquer forma isto parece um pouco cru e sem muito conteúdo, vamos adicionar um menu e uma página Sobre Mim

```powershell
echo [menu] >> hugo.toml
echo [[menu.main]] >> hugo.toml
echo identifier = "sobre" >> hugo.toml
echo name = "Sobre Mim" >> hugo.toml
echo url = "/sobre/" >> hugo.toml
```

Agora na pasta /content adicionamos o [sobre.md](http://sobre.md) e escrevemos o que queremos.

Um novo menu irá aparecer com a opção Sobre Mim e uma nova página 😀

![image.png](/images/criar-um-blog-em-hugo/Menu_Sobre.png)

O tema PaperMod tem muitas funcionalidades, como readtime, os menus, etc…

E com isto temos um Blog simples com a página inicial para listar posts e um sobre mim 😀

## Em resumo

Sites Estáticos são um excelente alternativa a sistemas de gestão de conteúdo, e ainda melhor, não vêm com uma price tag, é completamente gratuito e relativamente simples de começar!
Se estás à procura de como começar um blog ou migrar para uma alternativa de manutenção baixa Hugo é uma excelente alternativa.