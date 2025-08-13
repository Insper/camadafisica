## Instruções para Instalação da Infraestrutura

## Python

### Instalação do Python 3.x

#### Windows

1. Faça o download do Python no site oficial: [https://www.python.org/downloads/](https://www.python.org/downloads/)

2. Durante a instalação:

!!! warning "Importante"
    Marque a opção **"Add Python to PATH"** para instalar corretamente e permitir o uso do Python no terminal.

#### Linux

A maioria das distribuições Linux já vem com Python 3 instalado. Para verificar:

```bash
python3 --version
```

Se não estiver instalado, use o gerenciador de pacotes da sua distribuição:

```bash
# Ubuntu/Debian
sudo apt update && sudo apt install python3 python3-pip

# Fedora
sudo dnf install python3 python3-pip

# Arch Linux
sudo pacman -S python python-pip
```

#### macOS

O macOS já vem com Python instalado, mas recomenda-se instalar a versão mais recente:

1. Via Homebrew (recomendado):
```bash
brew install python
```

2. Ou baixe do site oficial: [https://www.python.org/downloads/](https://www.python.org/downloads/)

## Instalação dos Pacotes Python

Com o Python instalado, abra o terminal/CMD e execute os comandos abaixo:

### Windows
```cmd
pip install matplotlib numpy notebook pyserial
```

### Linux/macOS
```bash
pip3 install matplotlib numpy notebook pyserial
```

### Verificação da Instalação

Para verificar se os pacotes foram instalados corretamente:

```python
python -c "import matplotlib, numpy, notebook, serial; print('Todos os pacotes instalados com sucesso!')"
```

## Arduino IDE

### Instalação

1. Acesse o site oficial: [https://www.arduino.cc/en/software](https://www.arduino.cc/en/software)
2. Baixe a versão adequada para seu sistema operacional
3. Siga as instruções de instalação padrão

## WaveForms

### Instalação

1. Acesse: [https://digilent.com/reference/software/waveforms/waveforms-3/start](https://digilent.com/reference/software/waveforms/waveforms-3/start)
2. Baixe a versão adequada para seu sistema operacional
3. Execute o instalador seguindo as instruções padrão

!!! note "Nota"
    O WaveForms é usado para controlar dispositivos Digilent como o Analog Discovery 2.

