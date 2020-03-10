# Control Flow Graph (JavaScript)

### Basic block:
egy olyan programozási utasítás lineáris sorrendje, amelynek van egy
belépési pontja (az első végrehajtott utasítás) és egy kilépési pontja (a
utoljára végrehajtott utasítás).
A CFG egy irányított gráf, amelyben a csomópontok vannak, az élek pedig az útvonalakat képviselik.
Meghatározza az összes lehetséges végrehajtási utat.

[![N|Solid](https://thesafety.us/images/articles/javascript-logo.png)](https://nodesource.com/products/nsolid)

### CFG's
[STYX](https://github.com/mariusschulz/styx)


### Két kitüntetett blokk van, az ENTRY BLOCK és az EXIT BLOCK.

-belépési blokk (entry block)
Az a blokk, amin keresztül beléphetünk a gráfba

-Kilépési blokk (exit block)
Az a blokk, amin keresztül kiléphetünk a gráfból

-Visszamutató él (back edge)
Egy blokk ősére mutató él mélységi keresésnél (DFS)

-Kritikus él (critical edge)
Minden olyan él, amely nem hagyja el a forrás blokkját vagy lép be a célblokkjába. Új blokkok illeszthetőek be hasítás (új blokk létrehozása az él közepén) segítségével.

-Abnormális él (abnormal edge)
Az ismeretlen célú élek elnevezése. Gátolhatják az optimalizálást

-Lehetetlen él (impossible edge; fake edge)

A STYX Control Flow Gráfja ECMAScript 5 verziót használ(JavaScript)

AST (Abstract Syntax Tree) JavaScript forráskódból AST (Esprimát) állit elő
[AST](https://esprima.org/demo/parse.html)

[ESCONTROL](https://www.npmjs.com/package/escontrol)

[ESGRAPH](https://www.npmjs.com/package/esgraph)

[AST-FLOW-GRAPH](https://www.npmjs.com/package/ast-flow-graph)


# TESZT

Csináltam npm init-el egy új projektet. (npm init node-js project example)

    -npm install styx

    -npm install esprima

    -index.js - be beirtam a kódót

    -node index.js elinditottam

### ESPRIMA

-   parse függvény az inputból (string) csinál JavaScript AST-t
-   pl: input: "var x = 2+2";
-   output: 

Script {

  type: 'Program',

  body:

   [ VariableDeclaration {

       type: 'VariableDeclaration',

       declarations: [Array],

       kind: 'var' } ],

  sourceType: 'script' }

### STYX

-  control flow graphot csinál az AST-ből, amit pl az esprima parse függvényének az outputja
-  pl ha a styx parse függvényének odaadjuk az esprima parse függvényének az outputját, akkor az output:

{

  "program": {

    "flowGraph": {

      "nodes": [

        {

          "id": 1,

          "type": "Entry"

        },

        {

          "id": 2,

          "type": "SuccessExit"

        }

      ],

      "edges": [

        {

          "from": 1,

          "to": 2,

          "type": "Normal",

          "label": "x = 2 + 2",

          "data": {

            "type": "VariableDeclarator",

            "id": {

              "type": "Identifier",

              "name": "x"

            },

            "init": {

              "type": "BinaryExpression",

              "operator": "+",

              "left": {

                "type": "Literal",

                "value": 2,

                "raw": "2"

              },

              "right": {

                "type": "Literal",

                "value": 2,

                "raw": "2"

              }

            }

          }

        }

      ]

    }

  },

  "functions": []
  
}

A Styx verzió bővebb mint az Esprima.
ECMAScript 5-t használ (JavaScript)