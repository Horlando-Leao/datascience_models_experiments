# datascience_models_experiments

# Build Interactive Data Apps of Scikit-learn Models Using Taipy

## Descrição
Este repositório demonstra como construir aplicativos de dados interativos utilizando modelos do Scikit-learn e a biblioteca Taipy. O objetivo é fornecer uma interface interativa para visualização e manipulação de modelos de machine learning.

## Estrutura do Projeto
- **config.py**: Contém a função `configure` que define a configuração dos cenários.
- **interface.py**: Contém a definição da interface do usuário para o aplicativo Taipy.
- **main.py**: Script principal para configurar e rodar os cenários e a interface gráfica.

## Requisitos
- Python 3.x
- Scikit-learn
- Taipy

## Instalação
1. Clone o repositório:
    ```bash
    git clone https://github.com/seu-usuario/seu-repositorio.git
    cd seu-repositorio
    ```

2. Crie um ambiente virtual (opcional, mas recomendado):
    ```bash
    python -m venv env
    source env/bin/activate  # Linux/macOS
    env\Scripts\activate  # Windows
    ```

3. Instale as dependências:
    ```bash
    pip install -r requirements.txt
    ```

## Uso
1. Execute o script principal:
    ```bash
    python main.py
    ```

2. A interface gráfica estará disponível no navegador no endereço `http://localhost:3559`.

## Código
### main.py
```python
import taipy as tp

from time import time
from config import configure
from interface import interface
from taipy import Core, Gui
from sklearn.datasets import make_moons

if __name__ == "__main__":

    core = Core()
    my_scenario = configure()
    core.run()

    start = time()

    dataset = make_moons(noise=0.3, random_state=0)
    for model_name in ["MLPClassifier", "RandomForestClassifier", "SVC", 
                       "KNeighborsClassifier", "LogisticRegression",
                       "AdaBoostClassifier", "GradientBoostingClassifier",
                       "DecisionTreeClassifier", "GaussianNB"]:
        
        scenario = tp.create_scenario(my_scenario, name=f"{model_name}")
        
        scenario.X.write(dataset[0])
        scenario.y.write(dataset[1])
        scenario.model_name.write(model_name)

        tp.submit(scenario)

    print(f"Total time {time()-start}")

    # Instantiate, configure and run the GUI
    gui = Gui(pages={"/": interface})

    gui.run(dark_mode=False, port=3559, title="Taipy Scikit Demo App")
```

## Estrutura do Código
1. Inicialização e Configuração:

 - Core é inicializado e o cenário é configurado usando a função configure.
 - O dataset make_moons é gerado com ruído.
2. Criação e Execução de Cenários:

 - Para cada modelo de classificação, um cenário é criado, o dataset e o nome do modelo são escritos nas variáveis do cenário.
 - Cada cenário é submetido para execução.

3. Interface Gráfica:

 - A interface gráfica é configurada e executada usando a classe Gui da Taipy.
## Contribuição
 - Se você quiser contribuir, por favor, abra uma issue ou envie um pull request.

## Licença
Este projeto está licenciado sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.


