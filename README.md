# AwesomesCollectionsMultirepo
:globe_with_meridians: Awesomes Collections 

## Git Submodules explicação básica

### Por que submodulos?

No Git você pode adicionar um submodulo a um repositório. Este é basicamente um repositório incorporado em seu repositório principal. Isso pode ser muito útil. Algumas vantagens do uso de submodules:

- **Você pode separar o código em repositórios diferentes.**

     Útil se você tiver uma base de código com grandes componentes, você pode fazer um
     componente um submódulo. Desta forma, você terá um registro Git mais limpo
     (os commits são específicos para um determinado componente).

- **Você pode adicionar o submódulo a vários repositórios.**

     Útil se você tiver vários repositórios que compartilham o mesmo
     componentes. Com esta abordagem, você pode facilmente atualizar aqueles
     componentes em todos os repositórios que os adicionaram como um submódulo.
     Isso é muito mais conveniente do que copiar e colar o código no
     repositórios.

### Fundamentos

Quando você adiciona um submódulo no Git, você não adiciona o **código** do
submódulo ao repositório principal, você só adiciona **informações sobre o
submódulo** que é adicionado ao repositório principal. Essa informação
descreve para qual **commit o submódulo está apontando**. Assim, o
**código** do submódulo não será atualizado automaticamente se o submódulo
**repositório** é atualizado. Isso é bom, porque seu código pode não
trabalhar com o último commit do submódulo, evita
comportamento.


### Adicionando um submódulo

Você pode adicionar um submódulo a um repositório como este: 

    git submodule add git@github.com:url_to/awesome_submodule.git path_to_awesome_submodule

Com a configuração padrão, isso verificará o **código** do
repositório `awesome_submodule.git` para o` path_to_awesome_submodule`
diretório e **adicionará informações ao repositório principal** sobre
este submódulo, que contém o **comprometer os pontos do submódulo para**,
que será o commit **atual** do branch padrão (normalmente o
branch `master`) no momento em que este comando é executado.

Após esta operação, se você fizer um `git status`, verá dois arquivos em
a lista `Changes to be commit`: o arquivo` .gitmodules` e o caminho
para o submódulo. Quando você confirma e envia esses arquivos, você confirma / envia
o submódulo para a origem.

### Obtendo o código do submódulo

Se um novo submódulo é criado por uma pessoa, as outras pessoas no
equipe precisa iniciar este submódulo. Primeiro você tem que pegar o
**informações** sobre o submódulo, isso é recuperado por um normal
`git pull`. Se houver novos submódulos, você verá na saída de
`git pull`. Então você terá que iniciá-los com:

```
git submodule init
```

Isso irá puxar todo o **código** do submódulo e colocá-lo no
diretório para o qual está configurado.

Se você clonou um repositório que faz uso de submódulos, você deve
também execute este comando para obter o código do submódulo. Isso não é
feito automaticamente por `git clone`.

### Empurrando atualizações no submódulo

O submódulo é apenas um repositório separado. Se você quiser fazer alterações
a ele, você deve fazer as alterações neste repositório e enviá-las como
em um repositório Git regular (apenas execute os comandos git no
diretório do submódulo). No entanto, você também deve permitir que o **main**
repositório saiba que você atualizou o repositório do submódulo, e faça
ele usa o commit mais recente do repositório do submódulo. Porque se
você fizer novos commits dentro de um submódulo, o repositório **principal** irá
ainda **aponte para o antigo commit**.

Então, se você quiser ter essas mudanças em seu repositório **principal** também, você
deve dizer ao repositório **principal** para usar o último commit do
submódulo. Agora, como você faz isso?

Então você fez mudanças no repositório do submódulo e as confirmou
em seu repositório. Se você agora fizer um `git status` no **main**
repositório, você verá que o submódulo está na lista `Não muda
preparado para commit` e tem o texto `(conteúdo modificado)` por trás dele.
Isso significa que o **código** do submódulo é verificado em um
commit diferente do repositório **principal** está **apontando para**. Para
faça o **repositório** principal **apontar para** este novo commit, você apenas adiciona
esta alteração com `git add` e, em seguida, confirme e envie.

### Mantendo seus submódulos atualizados

Se alguém atualizou um submódulo, os outros membros da equipe devem atualizar
o código de seus submódulos. Isso não é feito automaticamente por
`git pull`, porque com` git pull` ele apenas recupera o
**informação** de que o submódulo está **apontando** para outro
**commit**, mas não atualiza o **código** do submódulo. Para atualizar o
**código** de seus submódulos, você deve executar:

    git submodule update


#### O que acontece se você não executar este comando?

Se você não executar este comando, o **código** do seu submódulo é verificado
para um commit **antigo**. Quando você faz `git status`, você verá o
submódulo na lista `Changes not staged for commit` com o texto
`(conteúdo modificado)` por trás dele. Não é porque você mudou o
código do submódulo, mas porque seu **código** é verificado em um
**commit**. Então, Git vê isso como uma mudança, mas na verdade você
apenas não atualizou o código do submódulo. Então, se você estiver trabalhando com
submódulos, não se esqueça de manter seus submódulos atualizados.


### Tornando mais fácil para todos

Às vezes é irritante se você se esquece de iniciar e atualizar seu
submódulos. Felizmente, existem alguns truques para tornar isso mais fácil:

     git submodule update --init

Isso atualizará os submódulos e, se ainda não forem iniciados,
iniciá-los.

Você também pode ter submódulos **dentro** de submódulos. Neste caso você
deseja atualizar/iniciar os submódulos recursivamente:

     git submodule update --init --recursive

É muito para digitar, então você pode fazer um alias:

     git config --global alias.update '! git pull && git submodule update --init --recursive'

Agora, sempre que você executar `git update`, ele executará um` git pull` e
um `git submodule update --init --recursive`, atualizando assim todo o código
no seu projecto.

---

## Referências

[Git Submodules](https://gist.github.com/gitaarik/8735255)

[Git Tools Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)





