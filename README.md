# CSS-Styleguide

Este projeto tem como objetivo a criação de um guia para desenvolvimento de códigos `CSS`. Para a construção deste guia, foi utilizado como base o guia de estilos da empresa [Airbnb](https://github.com/airbnb/css), de artigos encontrados online e também de acordo com a minha preferência/ajustes.

Toda e qualquer mudança/melhoria serão aceitas! O objetivo é melhorar o guia e, o mais importante, melhorar o fluxo de trabalho e organização dos projetos.

Se você tem alguma sugestão, dica, ideia, envie sua proposta de mudança! :)

> Nota: Sempre que busco inserir algo nesse guia, eu sigo as seguintes considerações:
> O que mudar?
> Por que?
>
> Isso garante que eu busque uma explicação do por que determinada área precisa mudar. Em alguns casos, a busca do "Por que?" acaba demonstrando a irrelevância da mudança, ou guiando para outro caminho. Se possível, siga a mesma lógica.

> Nota: Esse guia foi escrito com base em um ambiente de projeto gerenciado por SASS (ou algum outro processador) que proporcione a segmentação de arquivos, ordenação e concatenação dos mesmos durante o processo de build do projeto. Se você utiliza apenas um arquivo css, ou não utiliza processadores, algumas áreas desse guia não serão aplicáveis ao seu projeto.

## Tabela de conteúdo:

- [Estrutura](#estrutura)
    + [Pastas](#pastas)
    + [Arquivos](#arquivos)
- [Formatação](#formatação)
- [Comentários](#comentários)
- [Nomenclatura](#nomenclatura)
- [Variáveis](#variáveis)
- [Javascript hooks](#javascript-hooks)
- [Declarações](#declarações)
- [Ordem](#ordem)
    + [Arquivos](#arquivos)
    + [Regras](#regras)
- [!important](#important)
- [z-index](#z-index)
- [@media](#media)

## Estrutura

A estrutura de pastas e códigos é muito importante para manter um código bem organizado, de fácil manutenção, leitura e fácil de se encontrar. Isso é ainda mais importante quando trabalhamos dentro de um time de desenvolvimento, onde diversas pessoas trabalham em cima dos mesmos arquivos.

### Pastas

Para a estrutura de pastas, iremos usar o modelo a seguir:

> Nota: É importante que a ordem das pastas seja mantida no momento de compilar o código gerando um único css, assim o código não irá quebrar;

- funcoes: Contém todas as declarações de `functions`, `mixin` ou semelhantes;
- variaveis: Contém todas as declarações de variáveis em escopo global;
- reset: Contém os arquivos de reset da folha de estilo;
- ui: Contém estilos referentes a elementos únicos, que não montam um grupo/bloco extenso de estilo. Ex.: Botões, inputs, divisores, label, etc...
- component: Contém componetes que dependem de uma composição elaborada, necessitam de mais de um elemento para se compor. Ex.: produto, noticia, grid, nav, etc...
- view: Contém todo o layout correspondente a uma view exclusiva. É semelhante ao `component`, porém se refere a uma view exclusiva e não a um componente HTML. Ex.: inicio, contato, sobre nós, etc...

*Por que?* Essa estrutura garante uma boa organização e segmentação do código, além de garantir que ele seja ordenado conforme necessidade de uso. Ex.: Você precisa declarar a variável global antes de aplicá-la ao seu layout.

### Arquivos

É recomendado que para a criação da estrutura de arquivos seja utilizado um arquivo por objetivo. Caso seja necessário a criação de um estilo diferente, ou que envolva outro componente, deverá ser utilizado um novo arquivo.

É recomendado que a extensão utilizada para o arquivo seja `.scss`, deste modo podemos utilizar a syntax de declarações como variáveis, mixin, function, etc.

Também é recomendado que o nome do arquivo possua o prefixo `_` seguido do mesmo nome utilizado na declaração da classe.

**Evitar**

    estilos.css

**Recomendado**
    
    _produto.scss
    _noticia.scss
    _grid.scss

Exemplo de uma estrutura elabora:

- funcoes
    + _function.scss
    + _mixin.scss
- variaveis
    + _base.scss
    + _cor.scss
    + _typo.scss
    + _margem.scss
    + _border.scss
- reset
    + _normalize.scss
- ui
    + _button.scss
    + _fab.scss
    + _link.scss
    + _label.scss
- component
    + _produto.scss
    + _noticia.scss
    + _header.scss
    + _nav.scss
- view
    + _inicio.scss
    + _contato.scss
    + _empresa.scss

*Por que?* A utilização de um arquivo por classe ajuda a manter o seu código fácil de ser encontrado e fácil de se identificar o que cada arquivo possui.

*Por que?* Ao utilizar o mesmo nome para o arquivo e classe, você evita a criação de classes duplicadas, visto que ao criar 2 arquivos com o mesmo nome, não será possível salvar (ou irá sobrescrever um).

## Formatação

- Use 4 espaços para identação;
- Use traços ao invés de metodologia `camelCase` para nomear as classes;
    + O uso de `camelCase` ou `PascalCasing` podem ser usados para a primeira declaração, no caso de se adotar uma metodologia semelhante a `BEM`;
- NÃO USE seletores ID;
- Cada propriedade de um seletor deve ir em uma nova linha;
- Sempre use um espaço antes de abrir as chaves `{`;
- Em propriedades, coloque um espaço depois, mas não antes, dos dois pontos `:`;
- Coloque a chave de fechamento de um seletor `}` em uma nova linha;
- Utilize uma linha em branco entre declarações de regras;
- Utilize no máximo 3 níveis de aninhamento (quando estiver utilizando declarações que permitam aninhamentos);

*Por que?* Utilize espaços ao invés de `tab`, deste modo, não importa qual editor outro usuário esteja utilizando, o seu código não terá uma apresentação diferenciada com base na tabulação usado por outras pessoas.

*Por que?* Deixa o código mais segmentado, melhorando sua legibilidade, manitenção e entendimento para futuros desenvolvedores.

**Evite**

    .foo{
        display : inline; color: #000; }
    .nao, .faca, .isso {
        //-
    }
    #isso-aqui-nem-pensar {
        //-
    }
    .aninhe {
        //-
        .ate {
            //-
            .aqui {
                //-
                //- STÁPH!
                .nao-chegue-aqui {
                    //-
                }
            }
        }
    }

**Recomendado**

    .foo {
        display: inline;
        color: #000;
    }

    .um,
    .seletor,
    .por-linha {
        //-
    }

## Comentários

O comentário deverá ser utilizado no início do arquivo para descriminar o objetivo do `css`. Fora esse caso, os comentários devem ser evitados ao máximo! O comentário deverá seguir o modelo:

    /**
     * @Título
     * @Autor
     * @Data
     *
     * @Descrição
     * Descrição do arquivo e objetivo das regras
     */

Case seja necessário utilizar um comentário dentro de uma regra de declaração é recomendado que:

- Utilize comentário por linha `//`;
- Utilize o comentário em uma nova linha, evite que ele fique ao final da declaração;
- Opte por comentar apenas casos que o comentário agregue, ex.: Uso de `z-index`, prefixos, compatibilidade, etc.

**Evitar**

    .minha-classe {
        //Agora vou declarar uma classe nova
        display: inline-block;
    }

**Recomendado**

    .minha-classe {
        //Essa classe possui index 90 para sobrepor o alert em `affix` na lateral
        z-index: 90;
    }

*Por que?* Os comentários dentro de um arquivo css não possuem tanta importância visto que as declaração são auto explicativas. Utilize apenas para declarar qual o objetivo geral do arquivo, visto que por vezes é necessário a criação de uma classe mais extensa e não tão objetiva, por exemplo: `.ListaUsuarios {}`. Lista de que? usado aonde? usuários ativos? inativos?

*Por que?* Comentários são difíceis de continuar com manutenção e em muitas vezes são desnecessários ou não agregam conteúdo ao seu código.

## Nomenclatura

Existem diversas convensões de nomenclatura de seletores, sendo as mais famosas [OOCSS](https://github.com/stubbornella/oocss/wiki) e [BEM](http://getbem.com/introduction/). Considerando o fato de que isso não é uma regra a ser seguida a risca, podemos montar nossa própria metodologia, modificar e ou adotar uma já existente. Para esse projeto, iremos usar como base as metodologias `OOCSS` e `BEM`, com algumas modificações. Motivos pelos quais iremos nos basear nessas metodologias:

- Ajuda a criar uma relação mais clara e objetiva entre CSS e HTML;
- Ajuda na criação de componetes que podem ser reutilizados;
- Proporciona um CSS que não contenha um aninhamento profundo;
- Ajuda na criação de estilos que possam escalar;

Neste projeto, usaremos a seguinte estrutura de nomenclatura:

    <article class="noticia noticia-destaque">
        <h1 class="noticia_titulo-importante">Brasil venco jogo.</h1>

        <div class="noticia_conteudo">
            <p>...</p>
        </div>
    </article>

    <ul class="ListaUsuario">
        <li></li>
    </ul>

- `noticia` é a declaração do "Bloco" de notícia, sempre será o bloco de maior nível;
- `ListaUsuario` ou `listaUsuario` é a declaração do "Bloco". Como possui um nome composto e não indica um elemento descendente, se utilizarmos `lista_usuario` pode haver confusão;
- `noticia_titulo` é um "Elemento" do bloco notícia, representa uma declaração dependente que ajuda na criação do componente como um todo;
- `noticia_titulo-importante` e `noticia-destaque` são "Modificadores" e servem para alterar apenas uma pequena parcela do estilo, dando uma característica diferente ou variação de estado, apesar de seguir um mesmo padrão de design;

A utilização de seletores ID `#` devem ser evitadas ao máximo! O principal motivo para isso é o alto nível de especificidade que ele gera para as regras de declaração, fazendo com o `css` não tenha tanto reuso quanto desejado.

*Por que?* Não há necessidade de utilizar duplo traço `meu--modificador` ou duplo _underscore_ `meu__elemento`, podemos utilizar apenas `meu-modificador` e `meu_elemento`.

*Por que?* Utilizando este modelo conseguimos distinguir facilmente quando uma classe determina um novo bloco, quando determina um elemento dependente e quando determina uma modificação a um elemento já declarado anteriormente.

*Por que?* Evita que criemos classes para modificar elementos constantemente, criando uma ninhagem extensa de declarações para suprir/corrigir declarações sobrepostas;

*Por que?* Outras linguagens, como JS e jQuery também utilizam `camelCase` e/ou `PascalCase`, deste modo podemos distinguir melhor de onde cada um vem;

## Variáveis

As declarações de variáveis devem ser feitas preferencialmente no contexto global, deste modo elas podem ser utilizadas em diversas áreas da aplicação, mantendo harmonia no design. Busque utilizar traços para nomear as variáveis.

**Evite**

    $corPrincipal: #fff;

**Recomendado**

    $cor-principal: #fff;

Se for necessário a declaração de variáveis dentro de um arquivo que não seja o de variáveis, e você tenha certeza que ela não será utilizada fora daquele escopo (por exemplo, uma variável exclusiva das notícias), utilize o prefixo `_`;

**Evite**

    $noticiaGrande: 40px;
    $noticia-pequena: 20px;

**Recomendado**

    $_noticia-grande: 40px;
    $_noticia-pequena: 20px;

*Por que?* Deste modo podemos identificar qual varíavel pertence ao escopo global (vem de outro arquivo) e qual pertence ao escopo local (declarada no mesmo arquivo), podendo ser alterada sem grandes consequências.

## JavaScript hooks

Ao utilizar JavaScript que precise selecionar elementos na página, evite utilizar a mesma declaração de classe para servir como regra de declaração e parâmetro para o JS. Isso pode causar confusão ou deixar o design incorreto devido ao uso desordenado de classes, com objetivos distintos.

Neste caso, é compreesível e recomendável o uso de seletores ID, visto que só serão declarados no arquivo HTML e JS e só servem para localizar um elemento na página.

**Evite**

    .minha-classe {
        border: 2px solid #cde;
    }

    <div class="minha-classe">
        //-
    </div>

    var div = document.getElementsByClassName('minha-classe');

**Recomendado**

    .minha-classe {
        border: 2px solid #cde;
    }

    <div id="meuSeletor" class="minha-classe">
        //-
    </div>

    var div = document.getElementById('meuSeletor');

*Por que?* Mantém seu código mais limpo e objetivo, garantindo que você selecione o elemento desejado.

*Por que?* Garante que o seu layout não seja interferido por um objetivo ao qual aquela classe não foi designada.

## Declarações

Quando possível, evite o uso da palavra `none` e declare como `0`.

**Evitar**

    .minhaClasse {
        border: none;
    }

**Recomendado**

    .minhaClasse {
        border: 0;
    }

*Por que?* Propriedades com declarações numéricas devem ser "anuladas" de modo numérico.

## Ordem

A ordenação de regras e declarações é tão importante quanto a ordem estrutural, pois garante melhor manutenção no código.

### Arquivos

Ao criar um novo arquivo, busque por ordená-los da seguinte maneira:

- Variáveis;
- Regras;

**Evite**

    .uma-classe {
        color: $cor-principal;
    }

    //Declaração de uma nova cor
    $corSecundaria: #eeefff;

    .outra-classe {
        color: $corSecundaria;
    }

**Recomendado**

    /**
     * @Título
     * @Autor
     * @Data
     *
     * @Descrição
     * Descrição do arquivo e objetivo das regras
     */

    $_cor-secundaria: #eeefff;
    $_largura-especial: 120px;

    .uma-classe {
        color: $cor-principal;
    }

    .outra-classe {
        color: $_cor-secundaria;
    }

*Por que?* Deste modo você garante melhor organização, pois irá declarar primeiro todas as variáveis logo no início do arquivo, possuindo melhor manutenção.

*Por que?* Se você precisar alterar uma variável local futuramente, não precisará "caçar" no meio do arquivo, pois sabe que está declarada no início.

### Regras

A declaração de regras também é importante para que melhore a manutenção e leitura do seu código. Por isso usaremos a seguinte ordem:

- Propriedades [a -> z];
- @Include;
- Seletores especiais, ex.: `.classe:hover`, `.classe + p`;
- Seletores aninhados com dependência direta, ex.: `.classe.modificador`;
- Seletores aninhados com base em atributo, ex.: `.classe h1`;
- Seletores aninhados com declaração de filho (`child`), ex.: `.classe .modificador`;
- NADA vai após um seletor filho;

**Evitar**

    .classe {
        display: inline-block;
        border-top: 0;
        @include sombraComum;
        margin-bottom: 20px;
        &.modificador {
            display: none;
        }
        h1 {
            color: white;
        }
        + p {
            font-size: 24px;
        }
    }

**Recomendado**

    .classe {
        border-top: 0;
        display: inline-block;
        margin-bottom: 20px;
        @include sombraComum;
        + p {
            font-size: 24px;
        }
        &.modificador {
            display: none;
        }
        h1 {
            color: white;
        }
    }

*Por que?* Você obedece um nível de hierarquia lógico, com base na estrutura HTML. Facilita a compressão ao ler o código `css` e a entender como o mesmo está disposto no arquivo HTML.

*Por que?* Ao utilizar ordem alfabética, você sabe onde cada propriedade estará, pois segue uma linha de fácil entendimento.

## Important

`!important` não é importante! Se você está utilizando isso, é bem provável que seu código sofre de algum defeito sério de organização. São raros os casos em que o uso de `!important` é aceitável, por isso tente ao máximo obter o resultado desejado com regras básicas de `css`.

*Por que?* O uso do `!important` cria o maior nível de especificidade no `css` e não poderá ser sobrescrito. Se você adotar essa prática para resolver todos os problemas de `css`, logo logo seu código não irá seguir uma linha lógica de hierarquia.

## z-index

Utilize um arquivo de variáveis para declarar todos os indexes que você possui. Também evite de começar a contagem em números elevados. É comum ver declarações iniciando em 9999, porém a contagem é completamente válida e terá o mesmo resultado se iniciada do número 1. Para garantir que os elementos possuem uma ordem lógica, vamos segmentar os índices por dezenas, onde cada componente deverá estar contido em uma dezena. Ex.: 10, 20, 30...

**Evite**

    .nav {
        z-index: 9999;
    }

    .notificacao {
        z-index: 10000;
    }

**Recomendado**

    //Arquivo de variáveis
    $z-nav: 10;
    $z-notificacao: 20;

    //Arquivo de componentes
    .nav {
        z-index: $z-nav;
    }

    .notificacao {
        z-index: $z-notificacao;
    }

*Por que?* Você garante que não existam elementos com índices extremamente altos, ficando difícil de entender onde estão localizados no plano 3D.

*Por que?* Ao organizar os índices em um único arquivo de variáveis, você pode controlar de modo fácil e objetivo qual o plano 3D que ele irá ocupar, criando os níveis de sobreposição adequados.

## Media

**Pendente**
