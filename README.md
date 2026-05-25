# 👻 Foge Foge

Jogo de terminal em C no estilo Pac-Man, onde o herói deve escapar dos fantasmas — ou destruí-los com pílulas explosivas.

---

## Estrutura do Projeto

```
fogefoge/
├── fogefoge.c / .h   # Lógica principal do jogo
├── mapa.c / .h       # Leitura, alocação e manipulação do mapa
├── ui.c / .h         # Renderização ASCII art no terminal
└── mapa.txt          # Arquivo de mapa (editável)
```

---

## Como Jogar

### Compilar (MinGW/GCC)

```bash
gcc fogefoge.c mapa.c ui.c -o fogefoge
./fogefoge
```

### Controles

| Tecla | Ação        |
|-------|-------------|
| `w`   | Mover para cima    |
| `s`   | Mover para baixo   |
| `a`   | Mover para esquerda |
| `d`   | Mover para direita  |
| `b`   | Explodir pílula    |

### Objetivo

- **Ganhar:** eliminar todos os fantasmas.
- **Perder:** ser alcançado por um fantasma.

---

## Elementos do Mapa

| Símbolo | Elemento         |
|---------|-----------------|
| `@`     | Herói           |
| `F`     | Fantasma        |
| `P`     | Pílula explosiva |
| `.`     | Espaço vazio    |
| `|`     | Parede vertical  |
| `-`     | Parede horizontal|

---

## Mecânicas

- **Fantasmas** se movem aleatoriamente a cada turno.
- **Pílula:** ao passar por cima de um `P`, o herói a coleta. Pressionar `b` dispara uma explosão em cruz de até 3 casas em cada direção, destruindo paredes e fantasmas no caminho.
- O mapa é lido do arquivo `mapa.txt` e pode ser editado para criar fases personalizadas.

### Formato do `mapa.txt`

```
<linhas> <colunas>
<conteúdo linha por linha>
```

Exemplo:
```
6 10
|--------|
|FFF|....|
|........|
|FF...@|.|
|..F...|.|
|--------|
```

---

## Implementação

- Alocação dinâmica de memória para a matriz do mapa (`malloc`/`free`).
- Movimentação dos fantasmas via cópia do mapa a cada turno, evitando conflitos de movimento.
- Explosão da pílula implementada recursivamente (`explodepilula2`).
- Renderização com ASCII art de 4 linhas de altura por célula.
