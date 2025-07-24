## Introdução

Sabe quando você sente que está fazendo as coisas do jeito mais difícil no Pandas?
Pois é… tem umas funções meio “escondidas” que pouca gente usa, mas que deixam seu código muito mais rápido e fácil de entender.
Hoje eu vou te mostrar 5 dessas funções mágicas.
Bora lá?

## 1. pd.eval() — Avaliação eficiente de expressões

Imagina que o Pandas é uma calculadora gigante. O pd.eval() deixa ele fazer contas direto com strings, tipo uma fórmula.
Isso é bom porque ele calcula tudo rapidinho, até em grandes tabelas.
Exemplo:

```
pd.eval("df['col1'] + df['col2']")
```

### O que está acontecendo?

- Estamos dizendo: “Some os valores da coluna col1 com os valores da coluna col2”.

- O pd.eval() pega essa fórmula escrita como string (texto entre aspas) e calcula de forma mais rápida do que se você usasse df['col1'] + df['col2'] direto.

### Por que isso é útil?

- Em datasets grandes, pd.eval() usa menos memória e pode ser até mais rápido.

- Ele funciona bem com contas simples ou expressões maiores — sem precisar escrever tudo no estilo “colchete-coluna-colchete”.

É mais rápido do que somar coluna por coluna.

## 2. df.query() — Filtros legíveis e performáticos

Sabe quando você faz um filtro tipo df[df['idade'] > 18]?
Com query() fica muito mais limpo:

```
df.query("idade > 18")
```

### O que está acontecendo?

- Estamos dizendo ao Pandas: “Me mostre só as linhas onde a idade é maior que 18”.

- A diferença é que, em vez de usar df[df['idade'] > 18], usamos uma string simples dentro do query().

### Por que isso é útil?

- Fica mais fácil de ler e escrever.

- Com filtros maiores (ex: com 3 ou mais condições), o código com query() continua limpo e claro.

É como se você estivesse falando com o Pandas em português.
E ainda roda mais rápido quando o dataset é grande.

## 3. df.pipe() — Composição de funções para pipelines

Se você gosta de deixar o código organizado em etapas, o pipe() é perfeito.
Ele passa o DataFrame de uma função pra outra, tipo uma esteira de fábrica.
Exemplo:

```
df.pipe(limpa_dados).pipe(filtra_clientes).pipe(gera_relatorio)
```

### O que está acontecendo?

- Estamos empilhando funções: o df (nosso DataFrame) passa por limpa_dados(), depois por filtra_clientes(), e por fim por gera_relatorio().

É como se fosse isso:

```
temp = limpa_dados(df)
temp = filtra_clientes(temp)
resultado = gera_relatorio(temp)
```

### Por que isso é útil?

- Ajuda a escrever código em etapas claras, como um passo a passo.

- Isso facilita testes e manutenção — especialmente em pipelines de dados.

Fica fácil de entender e manter.

## 4. df.at[] e df.iat[] — Acesso super rápido a valores individuais

Imagina que o Pandas é tipo uma tabela gigante, e você quer pegar ou mudar só um valor, bem específico.
Pra isso, o jeito mais rápido e direto é usar at[] ou iat[] — como se fosse um atalho turbo pra um ponto exato da tabela.

at[]: acessa pelo rótulo (tipo nome da linha e coluna)

```
df.at[3, 'nome']
```

### O que está acontecendo?

- Acessa o valor da linha 3, coluna 'nome' — usando o nome da coluna.

- Como se dissesse: “Pega o nome da terceira pessoa da lista”.

iat[]: acessa pela posição (linha 0, coluna 1, por exemplo)

```
df.iat[3, 1]
```

### O que está acontecendo?

- Pega o valor na posição da linha 3 e coluna 1 (por índice, como nas listas Python).

- Ou seja: linha 3, coluna 1, independente do nome da coluna.

### Mas por que não usar loc[] ou iloc[]?

Boa pergunta! Olha só:

| Método   | Para quê serve?                      | É rápido?          |
| -------- | ------------------------------------ | ------------------ |
| `loc[]`  | Acessa valores usando **rótulos**    | Mais lento         |
| `iloc[]` | Acessa usando **posições numéricas** | Mais lento         |
| `at[]`   | Um único valor com rótulo            | **Mais rápido** ✅ |
| `iat[]`  | Um único valor com posição           | **Mais rápido** ✅ |

- at[] e iat[] são mais rápidos porque foram feitos só pra acessar UM valor, enquanto loc[] e iloc[] podem lidar com vários valores de uma vez (linhas, colunas, fatias etc.).

Tipo um teletransporte direto pro valor que você quer!

## 5. df.explode() — Transformar listas em linhas

Tem uma coluna que guarda listas? Tipo gêneros musicais: ['rock', 'metal']?
O explode() transforma isso em várias linhas, uma pra cada item da lista.
Assim dá pra analisar separado, sem fazer gambiarra.
Exemplo:

```
df.explode("generos")
```

### O que está acontecendo?

- Imagina que você tem uma linha assim:

```
{"nome": "Filipe", "generos": ["rock", "metal", "prog"]}
```

- O explode() transforma isso em 3 linhas:

```
{"nome": "Filipe", "generos": "rock"}
{"nome": "Filipe", "generos": "metal"}
{"nome": "Filipe", "generos": "prog"}
```

### Por que isso é útil?

- Isso facilita análises separadas por item (como contar quantos escutam “metal”).

- Evita loops ou códigos complicados — é só um comando.

Simples e poderoso!

## Conclusão

Usar essas funções é como encontrar atalhos secretos no seu jogo favorito.
Você chega no mesmo lugar, mas muito mais rápido — e com um código bem mais bonito.
Não precisa decorar tudo agora, salva esse post e volta quando estiver limpando ou analisando dados no Pandas.
Garanto que uma dessas vai te salvar!

Curtiu essas dicas? Ele foi gerado por inteligência artificial, mas revisado por alguém 100% humano

Me segue no [GitHub](https://github.com/FilipeMadeira13) e no [LinkedIn](https://www.linkedin.com/in/carlos-filipe-madeira-de-souza-16211922a/) pra mais conteúdos direto ao ponto sobre Python, Análise de Dados e Tech!

### Fontes de produção:

- Ilustrações de capa: gerada pela lexica.art
- Conteúdo gerado por: ChatGPT e revisões humanas

#PandasTips #PythonParaDados #DataScienceNaPrática
