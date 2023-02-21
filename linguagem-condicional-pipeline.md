O script não ficou bom, preciso que ele seja criado novamente, considerando a condição da linguagem dos arquivos que foram modificados no ato do push


Claro, aqui está um exemplo de um script de pipeline do Bitbucket que verifica a linguagem dos arquivos modificados no push e executa etapas específicas de acordo com a linguagem:

bash

~~~~bash
#!/bin/bash

# list of modified files
MODIFIED_FILES=$(git diff --name-only $BITBUCKET_COMMIT_PREV..$BITBUCKET_COMMIT)

# loop through each file and check the file extension
for file in $MODIFIED_FILES
do
    extension="${file##*.}"
    case $extension in
        "js")
            echo "JavaScript file found, running frontend build steps"
            # Frontend build steps
            ;;
        "py")
            echo "Python file found, running backend build steps"
            # Backend build steps
            ;;
        *)
            echo "No relevant file found"
    esac
done
~~~~


Este script usa o comando git diff --name-only $BITBUCKET_COMMIT_PREV..$BITBUCKET_COMMIT para obter uma lista de arquivos modificados desde o último commit, e então usa um loop para iterar sobre cada arquivo na lista.

Para cada arquivo, é extraída a extensão do arquivo usando a sintaxe de bash ${file##*.} e então é verificado se é uma extensão de arquivo relacionado a frontend ou backend. Se for "js" é considerado um arquivo relacionado a frontend e é executado alguns passos, se for "py" é considerado um arquivo relacionado a backend e é executado outros passos.

É importante notar que essa abordagem depende da convenção de nomenclatura dos arquivos utilizada no seu projeto, e pode não funcionar corretamente caso essa convenção não seja seguida. Além disso, este script considera apenas arquivos javascript e python. Se houver outras linguagens em seu projeto, você pode adicioná-las ao script.
