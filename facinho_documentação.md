# Documentação Falhas da Facinho Smurfs

Com a minha busca na por falhas na [facinhosmurfs.com.br](https://facinhosmurfs.com.br) achei diversas aberturas e falhas, dentre elas:
* Apis Abertas
* Paginas e Arquivos JS abertas.
* Mysql e Tela de Login do Dashboard de Admin abertas.
* Front end base abertas.


## Apis abertas.
Uma simples vasculhada com o BurpSuite na página inicial da facinho, conseguimos perceber algumas apis com informações confidenciais sendo disponibilizadas para o usuário.
Um exemplo seria as informações do cupom de desconto:

![Api de cupom de desconto](/images/jubsz10.png)

## Páginas e Arquivos JS.
Bom, documentar todos os JS aberto seria muito trabalho, porém dentro dos que usam na pagina inicial,
acabam se referindo á outros na pasta "pages" assim então que descobrimos a base de imports.
exemplo: https://www.facinhosmurfs.com.br/js/produtos.js: import { validateEmail, translateSkinType } from ***'../pages/dashboard/js/utils.js'*** https://www.facinhosmurfs.com.br/pages/dashboard/index   
(vi que já tiraram do ar a pagina dashboard de pages, porém resolvi documentar mesmo assim.)
#### Pagina base do dashboard de admin:
![Pagina base aberta](/images/dashboardpages.png)
#### Administração de Cupons:
![Pagina base aberta](/images/cupons.png)
---
Por mais que estas páginas não tivessem resultando em nada pois são bases, verificando a api que elas estavam puxando:   
***BackEnd/exemplo***   
e mudando para:   
***api/exemplo***   
o resultado do Get mudaria, sendo assim apontando aonde os hackers deveriam atacar para mais informações confidenciais.

## Mysql e tela de login Dashboard de Admin.
Com os direcionamentos da página base e da inicial, nos apontando para diversos arquivos, um deles é a dashboard de Admin.   
### Por mais que tenham bloqueado o acesso para https://www.facinhosmurfs.com.br/dashboard/default-login
![Erro](/images/erro.png)   
### Entrando em https://www.facinhosmurfs.com.br/dashboard/index nos redireciona à mesma página.
![Dashboard](/images/dashboard.png)
#### Isto é extremamente preocupante, pois algum "Social Engineering" ou "Brute Force" poderia facilmente conceber acesso aos hacker à essas páginas.

### E em um simples script de achar subdomains foi encontrado o MYSQL da web aplicação.
![MySQL](/images/mysql.png)
#### Outro caso onde um "Brute Force" poderia facilmente ser uma forma de entrada de hackers.