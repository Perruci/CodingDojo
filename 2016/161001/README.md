# Dojo 2016.10.01

Hoje vamos fazer jogos! O objetivo deste Dojo é fazer uma versão bem simples do icônico _Space Invaders_, um clássico dos arcades usando o framework _Love2D_. Para aqueles que não sabem, este framework foi escrito em `C++`, e os jogos podem ser escritos usando a linguagem de script _Lua_.

Entregas
--------

### Primeira entrega ###

Faça a nave voar na parte de baixo da tela, e faça com que ela dê tiros. Espera-se que o jogador:

+ Ande para a esquerda apertando a tecla `a`;
+ Para a direita com a tecla `d`;
+ Atire com a tecla `k`.

Um artista renomado já fez a arte da nave para você! Não se preocupe em desenhar nada, somente a bala, mas isso é fácil, porque ela pode ser só um quadradinho mesmo.

### Segunda entrega ###

Faça aparecer vários inimigos na parte de cima da tela. Não precisam ser muitos, só precisamos de uns 5 que apareçam lá em cima e que eles movam em direção à parte de baixo da tela.

O _sprite_ do inimigo também já foi entregue pelo mesmo artista renomado, então não se preocupe em criar nada. Somente faça com que eles apareçam lá em cima.

### Terceira entrega ###

Destrua os inimigos com as balas. Isto é, quando uma bala tocar um inimigo, tanto o inimigo quanto a bala devem desaparecer. O jogo termina quando:
+ Todos os inimigos morrerem.
+ Algum inimigo chegar à parte de baixo da tela.

Introdução a Lua
----------------

Lua é uma linguagem de programação _brasileira_ e _open source_. Ela se diferencia por ser uma linguagem _baseada em protótipos_, assim como Javascript. Seu maior uso é voltado para a indústria dos _video games_, sendo a linguagem de script por trás de frameworks como Love2D, Corona e Pico-8.

``` lua
-- Isto eh um comentario

-- # Tipos basicos
print("Tipos basicos: ")
local a_boolean = true
local another_boolean = false
local und = a_boolean and another_boolean
local oder = a_boolean or another_boolean
local number = 2
local another_number = 5
print("5 / 2 = " .. another_number / number) -- todos os numeros sao ponto flutuante!
local a_string = "hello"
local my_name = "joe"
local classic_string = a_string .. " " .. my_name .. "!"
print(classic_string)

-- # Estruturas de controle
print("Exemplo de if:")
if number > 3 then
    print(number)
elseif another_number ~= 5 then
    print(another_number)
else
    print("wtf dude")
end

print("For example:")
for i = 1, another_number do
    print("  " .. i)
end

print("Exemplo de while:")
local j = 0
while j < 10 do
    print("  " .. j)
    j = j + 3
end

function sayHello(name)
    return "hallo " .. name .. "!"
end
```

Como foi dito anteriormente, Lua é uma linguagem baseada em protótipos. Isto (basicamente, bem por cima) quer dizer que a única estrutura de dados usada é a `hash table`, chamada em Lua de `table`:

``` lua
-- # Tabelas
local tabela = { }
local lista = { }

for i = 1, 10 do
    table.insert(lista, i*2)
end

for i, it in ipairs(lista) do
    print("# " .. i .. ": " .. it)
end
print("Tamanho da lista: " .. (#lista))

tabela["nome"] = "Joe"
tabela.idade = 22

print("Tabela:")
for key, value in pairs(tabela) do
    print("  " .. key .. ": " .. value)
end
tabela.idade = nil
print("Tabela:")
for key, value in pairs(tabela) do
    print("  " .. key .. ": " .. value)
end

tabela.poder = sayHello
print(tabela.poder(tabela.nome))
```


Introdução a Love2D
-------------------

Love2D é um framework _open source_ para a criação de jogos 2D para diversas plataformas, incluindo Windows, Mac, Linux e Android.

Para se criar um projeto, cria-se uma pasta chamada `nome_do_jogo.love`. Dentro dela, precisamos criar no mínimo o arquivo `main.lua`, que será o ponto de início do nosso jogo:

``` lua

-- Estamos no arquivo nome_do_jogo.love/main.lua
function love.load()
    -- funcao que roda quando o jogo carrega. ela roda somente uma vez!
end

-- As funcoes update e draw rodam em loop ate que a aplicacao termine de alguma forma
function love.update()
    -- funcao que atualiza o estado do jogo antes de desenhar na tela
end

function love.draw()
    -- funcao que desenha na tela. as funcoes que desenham qualquer coisa somente podem vir aqui
end
```

Além deste arquivo, podemos ter um chamado `conf.lua` contendo algumas configurações da janela do jogo:

``` lua
function love.conf(t)
    t.title = "Example stuff"
    t.version = "0.10.1" -- Love2D version
    t.window.width = 600
    t.window.height = 400
end
```

Dentro arquivo `main.lua`, podemos usar o módulo `love`, contém as mais diversas funcionalidades para ser fazer um jogo:

``` lua
sound = love.audio.newSource("path/to/file.wav")
image = love.graphics.newImage("path/to/image.png")
love.audio.play(sound)
love.graphics.draw(image, 50, 60, 0, 1, 1)
love.graphics.setColor(255, 255, 255)
love.graphics.rectangle("fill", 300, 200, 50, 70)
if love.keyboard.isDown("right") then
    love.graphics.print("->")
end
if love.keyboard.isDown("left") then
    love.graphics.print("<-")
end

-- # docs for drawing functions
-- love.graphics.draw(image, x, y, 0, 1, 1)
-- love.graphics.rectangle("fill", x, y, width, height)
-- love.graphics.setColor(r, g, b)
```

Para rodar este jogo, rode o comando:

```
love nome_do_jogo.love
```

Referências
-----------

+ https://love2d.org/wiki/Main_Page
+ http://www.lua.org/manual/5.2/pt/
