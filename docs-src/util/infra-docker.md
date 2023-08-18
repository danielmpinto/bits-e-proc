# Configurando a Infra

A infraestrutura da disciplina utiliza Docker para rodar containers com imagens padronizadas com todas as ferramentas
instaladas e configuradas, de forma a ser mais prático, rápido e eficiente para o desenvolvedor.

Atualmente, containers é uma forma altamente popular e consolidada no mercado de software para distribuir sistemas, softwares, ambientes de desenvolvimento de forma padronizada.

=== "Windows"

    ## WSL2

    Abra o Command Prompt como administrador, encontre no menu iniciar, botão direito "Executar como administrador" e verifique a versão do Windows 10 instalada, através do comando `ver`. Você deverá ver algo como `10.0.xxxxxx`, sendo xxxxx a build do Windows, você precisa estar com 18362 ou superior. Se você tiver Windows 11, você não precisa verificar, visto que todas versões suportam o WSL2.

    1. Instale o WSL2 (Windows Subsystem for Linux): `wsl --install`
    2. Se você já tiver ele instalado, garanta que esteja atualizado: `wsl --update`
    3. Para garantir que o WSL rode sempre na versão 2, rode o comando: `wsl --set-default-version 2`

    ## Docker

    Agora, entre no site oficial do Docker, [https://www.docker.com](https://www.docker.com), e faça o download da última versão para Windows.

    1. Instale usando o instalador, sem mistério.
    2. Volte para o Command Prompt, e agora vamos baixar a imagem da infra:
    ```bash
    docker pull rafaelcorsi/bits
    ```
    3. Após concluído o processo, vamos agora testar a imagem rodando um container.
    ```bash
    docker run --rm -it rafaelcorsi/bits /bin/bash
    ```

    Se deu certo, você deve ter caído na linha de comando do bash, como se tivesse num ambiente Linux. Para confirmar que está na imagem correta, rode o comando:

    ```bash
    nextpnr-mistral
    ```

    ## OpenFPGALoader

    Para instalar o programador **openFPGALoader**, entre na página com os binários [https://github.com/trabucayre/openFPGALoader/releases](https://github.com/trabucayre/openFPGALoader/releases).

    1. Baixe a versão **mingw-w64-x86_64-openFPGALoader-ci-1-any.pkg.tar.zst**
    2. Extraia o arquivo utilizando o 7-zip ou algum outro aplicativo. Copie o arquivo **openFPGALoader.exe** para a pasta da disciplina ou coloque no seu PATH.
    3. Abra o Command Prompt novamente como administrador, entre na pasta da disciplina, rode o comando `openfpgaloader -V` no terminal e verifique se é exibido a versão.

    **Importante:** sempre que for utilizar da disciplina, ver se o Docker está aberto, caso contrário, a infra não funcionará.

=== "Mac OS (Intel ou ARM)"

    ## Docker

    Antes de começar, assegure-se de que seu sistema operacional é macOS na versão Big Sur (11) ou superior (como Monterey, Ventura, etc.). Para usuários do Mac com chipset M1, não se preocupe, todos são compatíveis.

    1. Acesse o [site oficial do Docker](https://docs.docker.com/desktop/install/mac-install/) e baixe o aplicativo Docker. Importante: existem duas versões para macOS, x64 e M1. Certifique-se de escolher a correta para o seu Mac.
    2. Execute o instalador e siga as instruções apresentadas.
    3. Uma vez instalado, abra o aplicativo Docker. Você pode localizá-lo na pasta 'Aplicativos' ou buscar no Spotlight usando o atalho Command+Space.
    4. Com o Docker em execução, abra o terminal do macOS (pode ser encontrado em 'Aplicativos' ou via Spotlight com Command+Space) e execute o comando:

    ```bash
    docker pull rafaelcorsi/bits
    ```

    5. Depois de concluir o download da imagem, teste-a executando um container:

    ```bash
    docker run --rm -it rafaelcorsi/bits /bin/bash
    ```

    6. Se tudo ocorreu corretamente, você estará no prompt do bash, como se estivesse em um ambiente Linux. Para garantir que você está na imagem correta, execute:

    ```bash
    nextpnr-mistral
    ```

    A execução deste comando deve retornar informações sobre a ferramenta **mistral**, utilizada para gerar códigos VHDL/Verilog.

    ## OpenFPGALoader

    Para a instalação do programador openFPGALoader, é necessário ter o **Homebrew** instalado. Confirme a instalação executando `brew --version` no terminal. Se o Homebrew estiver instalado, você verá a versão. Se não, siga as [instruções de instalação no site oficial](https://brew.sh/index_pt-br).

    1. Após ter o Homebrew instalado, use-o para instalar o openFPGALoader:

    ```bash
    brew install openfpgaloader
    ```

    > Nota: O Homebrew é um gerenciador de pacotes por linha de comando para macOS, similar aos sistemas Apt, DNF, Pacman e outros encontrados no Linux.

    2. Confirme a instalação do openFPGALoader com:

    ```bash
    openfpgaloader -V
    ```

    Este comando deve exibir a versão do programa.

    3. **Lembrete Importante:** Sempre que for trabalhar na disciplina, certifique-se de que o Docker esteja em execução. Caso contrário, a infraestrutura não funcionará.

=== "Linux (Ubuntu)"

    ## Docker

    1. No terminal, instale o Docker utilizando o seguinte comando:

    ```bash
    sudo snap install docker
    ```

    2. Habilite as permissões necessárias para o seu usuário:

    ```bash
    sudo addgroup --system docker
    sudo adduser $USER docker
    newgrp docker
    sudo snap disable docker
    sudo snap enable docker
    ```

    3. Com o Docker instalado e configurado, baixe a imagem desejada:

    ```bash
    docker pull rafaelcorsi/bits
    ```

    4. Após a conclusão do download, teste a imagem executando um container:

    ```bash
    docker run --rm -it rafaelcorsi/bits /bin/bash
    ```

    Se a operação for bem-sucedida, você estará no prompt do bash, emulando um ambiente Linux. Para certificar-se de que você está na imagem correta, execute:

    ```bash
    nextpnr-mistral
    ```

    A execução desse comando mostrará informações sobre a ferramenta **mistral**, que usamos para gerar códigos VHDL/Verilog.

    ## OpenFPGALoader

    1. Acesse [esta página](https://github.com/trabucayre/openFPGALoader/releases) e baixe a versão apropriada para a sua distribuição Ubuntu (20.04 ou 22.04). Se você estiver usando uma versão mais recente, como 22.10, tente a versão 22.04.

    2. Extraia os arquivos baixados e copie os diretórios relevantes:

    ```bash
    tar xf ubuntu22.04-openFPGALoader.tgz
    sudo cp -r ubuntu22.04-openFPGALoader/usr/ /usr/
    sudo cp -r ubuntu22.04-openFPGALoader/etc/ /etc/
    sudo chmod +x /usr/local/bin/openFPGALoader
    ```

    3. Para verificar a instalação bem-sucedida, execute o seguinte comando no terminal:

    ```bash
    openfpgaloader -V
    ```

    Se o comando retornar a versão do programa, a instalação foi bem-sucedida.
