## Descartando alterações no Working Directory: 

~~~
git checkout
~~~

Exemplo: 

A versão atual do nosso arquivo o nome "proposta_1.html" é: 

~~~
<html>
  <head>
    <title>Proposta N°1 para homepaga da empresa</title>
  </head>
  <body>
    <h1>Cabeçalho do sistema</h1>
    <div>
      Isso aqui é o conteúdo da página
    </div>
    <h6>Copyright - Robson Vinicius 2021</h6>
  </body>
</html>
~~~

O usuário "robsonvinicius" decide alterar a página, porém por acidente, ele troca a "/" por "\" na Tag </div>. O arquivo alterado ficou:

~~~
<html>
  <head>
    <title>Proposta N°1 para homepaga da empresa</title>
  </head>
  <body>
    <h1>Cabeçalho do sistema</h1>
    <div>
      Isso aqui é o conteúdo da página
    <\div>
    <h6>Copyright - Robson Vinicius 2021</h6>
  </body>
</html>
~~~

Ao visualizar a página, o usuário "robsonvinicius" percebeu que há um bug no sistema, mas ele não consegue encontrar onde está localizado o erro. 
Ao verificar o estado do sistema com o comando git status, ele verifica que só o arquivo "proposta_1.html" foi modificado e as alterações ainda
estão no "Working Directory". Então, ele decide descartar todas as alterações que foram realizadas desde o último commit, isto é, voltar o seu
sistema para o estado em que se encontra no HEAD. Uma opção seria verificar as alterações que foram feitas com o comando git diff e desfazer as
alterações manualmente. Mas e se muita coisa foi alterada dentro de um arquivo? Para este problema, o Git nos possibilita descartar todas as 
alterações que estão no "Working Directory" de um determinado arquivo. Para isso, utilizamos o comando git checkout passando o nome do arquivo cujas
alterações serão removidas. No nosso caso, temos:

~~~
git checkout proposta_1.html
~~~

A saída não devolve nada mas, ao realizar o comando git status, verificamos que não há mais alterações no arquivo "proposta_1.html" que estejam
no "Working Directory". Note que já utilizamos o comando git checkout antes para alternar entre as branches do repositório. A diferença entre os
dois é o argumento que passamos para o comando: se for o nome de uma branch, trocaremos de branch; mas se for o nome de um arquivo, deixaremos o
arquivo conforme ele se encontra no HEAD da branch atual.

Vimos que é uma boa prática desenvolver uma tarefa numa branch diferente da branch master, deixando-a apenas para sincronização com o repositório
remoto. Então, o usuário "robsonvinicius" criou a branch "desenvolvimento" e mudou para ela com o comando git checkout -b desenvolvimento.

Enquanto isso, a usuária "fernandaamaral" atualizou o repositório remoto modificando o arquivo "proposta_1.html". Ao realizar o git pull na branch
master, o usuário "robsonvinicius" recebeu a atualização que a "fernandaamaral" realizou. Agora, ele deseja utilizar a versão apenas do arquivo 
"proposta_1.html" que se encontra na branch master, deixando o resto dos arquivos intactos. Uma solução seria olhar o arquivo na branch master
e copiar o seu conteúdo para a branch desenvolvimento. Contudo, o Git já nos permite fazer tal operação de uma maneira mais simples: basta passar
ao comando git checkout o nome da branch e o do arquivo que se deseja copiar. No nosso caso, temos:

~~~
git checkout master proposta_1.html
~~~

Esse comando trará o arquivo "proposta_1.html" como ele se encontra na branch "master" e o adicionará ao Index do repositório na branch 
"desenvolvimento", pronto para um commit.
