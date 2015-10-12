# Contêiner Docker para trabalhar com sites Jekyll

Publicado no Docker Hub em : [https://registry.hub.docker.com/u/parana/jessie-jekyll/](https://registry.hub.docker.com/u/parana/jessie-jekyll/)

Este projeto foi testado com a **versão 1.8.2** do Docker

Usado no curso [http://joao-parana.com.br/blog/curso-docker/](http://joao-parana.com.br/blog/curso-docker/) criado para a Escola Linux.

O **Jekyll** é um gerador de códigos estáticos. Ele permite páginas ou 
até mesmo um site completo de forma estática, ou seja, usando apenas HTML. CSS e
JavaScript, linguagens que a maioria dos desenvolvedores já conhecem, 

O **Jekyll** vai ajudá-lo a converter seu site em arquivos 
estáticos, pronto para ser publicado à partir de conteúdo criado em vários 
outros formatos mais simples, como por exemplo o Markdown.

Ele usa o Template `Liquid` e YAML como forma de definir o conteúdo e o layout.

Todos os arquivos ou diretórios que tiver _ (underline) na frente do nome, 
será ignorarado no pacote final a ser entregue ao usuário do site. Eles são
considerados como a definição do site e o Jekyll esconde do usuário final.

A pasta _includes armazena arquivos que serão reutilizados nas páginas do 
projeto, tipo o header, o footer, o sidebar e etc.

Na pasta _layouts ficam os padrões de layout de páginas. 

Podemos usar o Yeoman para gerar a estrutura do site Jekyll. 

```
gem install bundler
npm install -g yo
npm install -g generator-jekyllized
npm install node-sass
npm rebuild node-sass
npm install
cd site
gulp build
```

**Isso já foi feito** e o resultado encontra-se no diretório `site`.

A estrutura de diretórios e os arquivos são de facil entendimento.
É preciso conhecer um pouco de YAML, que é um formato de serialização muito 
simples e de facil aprendizado.

## Diferencial do Jekyll

Não é necessário usar um banco de dados e é isso que faz toda a diferença.
O conteúdo do site fica armazenado nos arquivos HTML, SCC e JavaScript 
de cada página. Só existe dependência de FileSystem.

Exemplo de uso:

```
docker run --rm -i -t -v "$PWD/site:/src" parana/jessie-jekyll build
```

Para invocar várias vezes podemos definir um alias

```
alias jekyll='docker run --rm -v "$PWD/site:/src" -p 80:4000 parana/jessie-jekyll'
jekyll build
jekyll serve --w -H 0.0.0.0
```

Para rodar como Daemon, fazemos:
```
docker run -d -v "$PWD/site:/src" -p 80:4000 parana/jessie-jekyll serve -H 0.0.0.0
```

## Funcionalidades disponíveis
 - Highlighting de código fonte via pygments
 - Suporte a geração de páginas do Github Pages
 - Suporte ao Redirect do Jekyll (https://github.com/jekyll/jekyll-redirect-from)
 - Suporte à gramática Markdown via Kramdown - https://github.com/gettalong/kramdown
 - Suporte ao RDiscount, que converte documentos Markdown em HTML.
 - Suporte ao Rouge - Um highlighter de código escrito em Ruby que é compatível com pygments
 - Suporte ao redcarpet
 - Suporte ao bundler
