# COMO GERAR UM PASSWORD/SECRET KEY ALEATÓRIO

```
openssl rand -base64 32 | colrm 9
```

gera um password de tamanho 8.

ou uma key

```
openssl rand -base64 32
```
H2EP+NIFF0tHztPb23icCYTSutWYCmzImg6GjidPVhg=

# Comando colrm

Como usar o comando colrm?
Como já mencionado, o comando colrm permite remover colunas. Portanto, você só precisa especificar um valor numérico e a coluna correspondente a esse valor, bem como todas as colunas subsequentes, serão removidos na saída.

# Editor Config

https://editorconfig.org/

EditorConfig ajuda a manter estilos de codificação consistentes para vários desenvolvedores que trabalham no mesmo projeto em vários editores e IDEs. O projeto EditorConfig consiste em um formato de arquivo para definir estilos de codificação e uma coleção de plug-ins de editores de texto que permitem aos editores ler o formato do arquivo e aderir aos estilos definidos. Os arquivos EditorConfig são facilmente legíveis e funcionam bem com sistemas de controle de versão.

# INÍCIO

Crie o arquivo:

```yml
# EditorConfig is awesome: https://EditorConfig.org

# top-most EditorConfig file
root = true

# Unix-style newlines with a newline ending every file
[*]
end_of_line = lf
insert_final_newline = true

# Matches multiple files with brace expansion notation
# Set default charset
[*.{js,py}]
charset = utf-8

# 4 space indentation
[*.py]
indent_style = space
indent_size = 4

# Tab indentation (no size specified)
[Makefile]
indent_style = tab

# Indentation override for all JS under lib directory
[lib/**.js]
indent_style = space
indent_size = 2

# Matches the exact files either package.json or .travis.yml
[{package.json,.travis.yml}]
indent_style = space
indent_size = 2
```


