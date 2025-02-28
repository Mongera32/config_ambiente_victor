# Introdução

Use este guia para replicar todas as configurações básicas do ambiente do [Autor](https://github.com/Mongera32).

Este guia pressupõe conhecimendo básico sobre **instalação de sistemas operacionais** e **linguagens shell usadas no Linux**.

A menos que seja especificado o contrário, os blocos de código mostrados nesse guia são comandos **shell** que funcionam tanto com o **Bash** quanto com o **ZSH**.

## Sobre o Ambiente

| Componente | Software usado | Observação | Plugins |
|---|---|---|---|
| Sistema Operacional | [Endeavour OS](https://endeavouros.com) Mercury (2025.02.08) | - | - |
| Shell | [zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) | _framework_ [oh-my-zsh](https://ohmyz.sh) usado para gerenciamento de plugins | [git](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/git/git.plugin.zsh); [fzf](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/git/git.plugin.zsh); [Syntax Highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) |
| Desktop | [Gnome Desktop](https://www.gnome.org) | - | [Dash to Dock](https://micheleg.github.io/dash-to-dock/); [Pop Shell](https://github.com/pop-os/shell) | 

# Instalando Sistema Operacional

As etapas de [Personalização do Sistema](#per_sis) pressupõem que o sistema operacional instalado é o [Endeavour OS](https://endeavouros.com) com [Gnome Desktop](https://www.gnome.org). Essas etapas _podem_ funcionar com instalações diferentes, porém isso foge do escopo e não será explicado aqui. Instale o sistema operacional conforme descrito nos passos a seguir e depois opte ou não pelas [Configurações Opcionais](#rec_conf) e [Aplicativos](#aplicativos).

1. Baixe o _.iso_ no site [Endeavour OS](endeavouros.com) e crie uma mídia de instalação. Recomenda-se que a autenticidade do arquivo seja verificada através da [assinatura GPG](https://www.gnupg.org/gph/en/manual/x135.html) conforme instruções do site.

2. Bootar a mídia de instalação e, no wizard de instalação, selecionar a opção **instalação online**. Quando perguntado sobre o desktop desejado, selecionar **Gnome Desktop**.
    
3. Finalizar a instalação e reiniciar.


# Personalização do Sistema <a id="per_sis"></a>

As sessões a seguir mostram como personalizar o sistema da forma ideal para o caso de uso do [Autor](https://github.com/Mongera32) desse guia. Recomenda-se que o leitor use ou não as etapas de personalização a seguir conforme o próprio caso de uso e preferências pessoais.

## Configurações Recomendadas <a id="rec_conf"></a>

As instalações a seguir são altamente recomendadas para deixar o _Desktop_ mais amigável e o _workflow_ mais eficiente.

### ZSH, oh-my-szh e plugins <a id="zsh_conf"></a>

O shell [zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) é muito personalizável e seus plugins tornam o uso do terminal muito mais fácil. O _framework_ [oh-my-zsh](https://ohmyz.sh) é útil para gerenciamento de plugins e torna a interface do terminal mais estética.

O **Endeavour OS** não vem com o **zsh** instalado. Instale com o comando:
```
sudo pacman -S zsh 
```
Mude o shell padrão para o **zsh** com o comando:
```
chsh -s "$(which zsh)" "$(whoami)"
```
Por fim, instale o [oh-my-zsh](https://ohmyz.sh):
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

#### git

O plugin [git](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/git/git.plugin.zsh) já vem instalado e ativado com a instalação do [oh-my-zsh](https://ohmyz.sh). **Nenhuma ação é necessária**.

#### fzf

_fzf_ melhora o recurso de busca do shell ao usar _ctrl + R_ . Esse plugin já vem instalado com o [oh-my-zsh](https://ohmyz.sh), bastando ativá-lo editando o arquivo _~/.zshrc_ ou usando o seguinte comando no terminal para editá-lo automaticamente:
```
awk '/^plugins=\(/ {sub(/\)$/, " fzf)")} 1' ~/.zshrc > tmpfile && mv tmpfile ~/.zshrc 
```
É necessário reiniciar o terminal para que essa configuração faça efeito

#### Syntax Highlighting

_Syntax Highlinghting_ é um plugin que destaca a sintaxe dos comandos digitados no terminal. Use o seguinte comando para clonar o repositório no diretório de plugins do _oh_my_zsh_ e ativá-lo no arquivo _~/.zshrc_:
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
awk '/^plugins=\(/ {sub(/\)$/, " zsh-syntax-highlighting)")} 1' ~/.zshrc > tmpfile && mv tmpfile ~/.zshrc 
```
É necessário reiniciar o terminal para que essa configuração faça efeito

### Plugins do Gnome Desktop <a id="gnome_plugins"></a>

Os

#### Pop Shell

Ótimo _Tiling Window Manager_ com interface agradável e eficaz. Pode ser instalado usando do _Arch User Repository_ (AUR) com o comando:
```
yay -S gnome-shell-extension-pop-shell 
```
É necessário reiniciar a sessão para que a instalação faça efeito. Após reiniciar, abra o aplicativo **Extensões** na lista de aplicativos do **Gnome Desktop**.


#### Dash to Dock <a id="dash-to-dock"></a>

Permite grande flexibilidade para configurar o Dock do Gnome. Pode ser instalado usando do _Arch User Repository_ (AUR) com o comando:

```
yay -S gnome-shell-extension-dash-to-dock 
```
É necessário reiniciar a sessão para que a instalação faça efeito. Após reiniciar, abra o aplicativo **Extensões** na lista de aplicativos do **Gnome Desktop**.

## Aplicativos usados <a id="aplicativos"></a>

O uso ou não dos seguintes aplicativos varia conforme preferência do usuário e workflow. 

| Nome do app                             | Comando para instalação com pacman        |
| ---                                     | ---                                       |
| Slack Desktop                           | yay -S slack-desktop                      |
| VS Code (release da Microsoft)          | yay -S visual-studio-code-bin             |
| Steam                                   | sudo pacman -S Steam                      |
| Opera Browser                           | yay -S opera                              |


## Miscelânea

### Montagem de Partições

Para que todas as partições sejam montadas no boot, adicione uma linha no arquivo [/etc/fstab](https://wiki.archlinux.org/title/Fstab) com o seguinte formato:

_**identificação**_ _**ponto-de-montagem**_ _**tipo**_ defaults 0 0

| identificação | ponto-de-montagem | tipo|
| --- | --- | --- |
[UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) ou caminho absoluto da partição na pasta /dev. | Onde a partição será montada no sistema de arquivos. | Tipo do sistema de arquivos. Geralmente ext4 para sistemas Linux. |




### não mostrar lixeira e partições no Dock

As configurações a seguir exigem que antes seja feita a [instalação](#dash-to-dock) da extensão [Dash to Dock](https://micheleg.github.io/dash-to-dock/).

Por padrão, o _Dock_ do [Gnome Desktop](https://www.gnome.org) mostra os ícones da **lixeira** e de quaisquer **partições** montadas que não sejam do sistema. Siga os passos a seguir para que o Dock não mostre esses ícones:

Esconder a **lixeira**:
```
gsettings set org.gnome.shell.extensions.dash-to-dock show-trash false
```

Esconder as **partições**:
```
gsettings set org.gnome.shell.extensions.dash-to-dock show-mounts false
```





