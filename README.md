# Utilizando Web API

Este projeto tem como objetivo principal explorar e demonstrar o uso de diversas Web APIs. Atualmente, o foco está na integração com a API do **Open Route Service** para o cálculo de rotas.

---

### Sobre o Projeto

O projeto é um estudo prático de como consumir e processar dados de Web APIs de terceiros. A ideia é criar ferramentas e scripts que utilizem essas APIs para funcionalidades específicas.

---

### Funcionalidade Atual

* **Cálculo de Rotas**: Utiliza a Web API do Open Route Service para determinar a **duração** e a **distância** entre dois ou mais pontos.
* **Visualização de Rotas**: Gera mapas em PNG para visualizar as rotas calculadas.
* **Geração de Relatórios**: Cria um documento em PDF com todas as informações de distância, duração e os mapas das rotas.

---

### Exemplo de Resultado

Abaixo está um exemplo de um dos mapas gerados, mostrando a rota de Niterói para Paraty de carro.

![Exemplo de rota de Niterói para Paraty de carro](outputs/figures/mapa_driving-car_Paraty.png)

---

### Análise dos Resultados das Rotas (Comparação, Plausibilidade e Fatores Reais)

* **Comparação de Distâncias e Rotas:**
    * **Carro:** Geralmente oferece as rotas mais diretas e otimizadas para a rede viária de veículos, resultando nas menores distâncias em termos de percurso por estradas.
    * **Caminhada:** As distâncias podem ser menores que as de carro para percursos urbanos diretos (como Niterói ao Rio de Janeiro, se a API ignora a ponte e sugere uma travessia "hipotética" ou via barca sem calcular o trajeto real da barca), mas podem ser maiores para destinos mais distantes com caminhos menos otimizados para pedestres ou que exigem desvios por falta de calçadas.
    * **Bicicleta:** As distâncias ficam frequentemente entre carro e caminhada, pois podem utilizar algumas vias de carro e, idealmente, ciclovias, mas também podem ter restrições em rodovias ou vias de alta velocidade.
---
* **Plausibilidade das Durações (Tempo de Movimento Puro vs. Tempo Real):**
    * **Carro:** As durações para carro são, em geral, **otimistas**. Elas representam um "tempo de movimento puro", calculado com base nas velocidades médias permitidas nas vias, sem considerar o trânsito em tempo real. Em cidades como Rio de Janeiro e Niterói, e na subida da serra para Petrópolis, o congestionamento diário faz com que o tempo real de viagem seja significativamente maior do que o indicado pela API.
    * **Caminhada e Bicicleta (Longas Distâncias):** As durações para Petrópolis e Paraty nesses perfis são **plausíveis apenas como tempo de movimento contínuo/líquido**. É o tempo que levaria para cobrir a distância sem parar. Na prática, uma viagem de 15 horas (caminhada para Petrópolis) ou 54 horas (caminhada para Paraty) seria inviável para ser feita de forma contínua, exigindo múltiplas paradas para descanso, alimentação e sono ao longo de vários dias. Da mesma forma para bicicleta.
---
* **Fatores do Mundo Real Não Considerados pela API:**
    * **Trânsito e Congestionamentos:** A API não incorpora dados de tráfego em tempo real, que são cruciais para a duração real de viagens de carro em áreas urbanas e rodovias movimentadas.
    * **Condições da Infraestrutura:** Não considera a qualidade das calçadas para caminhada, a existência e qualidade de ciclovias, trechos perigosos ou inviáveis para pedestres/ciclistas (como a Ponte Rio-Niterói para esses modais sem a barca).
    * **Barreiras Geográficas e Meios de Travessia:** Para a rota Niterói-Rio de Janeiro a pé ou de bicicleta, a API não "entende" que a travessia da Baía de Guanabara é geralmente feita por barca, e não por uma rota terrestre direta (que seria muito mais longa ou inexistente/insegura para esses modais).
    * **Paradas e Descanso:** As durações são de movimento ininterrupto. Viagens longas exigem pausas para alimentação, hidratação, descanso, pernoite (para caminhada/bicicleta), e essas paradas aumentam o tempo total da jornada.
    * **Relevo e Condição Física:** Embora o perfil `cycling-regular` tente considerar o relevo, a intensidade da subida da serra para Petrópolis pode ser subestimada para um ciclista médio, afetando o tempo real. A condição física individual também é um fator não considerado para caminhada e bicicleta.
    * **Variáveis Climáticas:** Chuva, vento forte ou calor excessivo podem impactar significativamente a velocidade e a duração de viagens a pé ou de bicicleta, e não são considerados pela API de roteamento.

---

### Como Usar (Notebooks Jupyter)

Para rodar os códigos e explorar o projeto, você precisará de um ambiente que suporte notebooks Jupyter, como o JupyterLab ou VS Code.

**Passo 1: Obtenha sua chave da API**

Para obter sua chave, visite [https://account.heigit.org/login](https://account.heigit.org/login), crie uma conta e gere uma nova chave de API.

**Passo 2: Crie os arquivos de configuração**

Antes do primeiro commit, siga estes passos para garantir a segurança da sua chave de API:

1.  Crie um arquivo chamado **`.env`** na raiz do seu projeto. Dentro dele, adicione a sua chave da API.
    
    ```
    # Exemplo de conteúdo do arquivo .env
    ors_api_key = 'SUA CHAVE AQUI'
    ```

2.  Crie um arquivo chamado **`.gitignore`** também na raiz do seu projeto. Adicione a linha abaixo para instruir o Git a ignorar seu arquivo de chaves, impedindo que ele seja enviado para o repositório.
    
    ```
    # Ignora arquivos de variáveis de ambiente
    .env
    ```

**Passo 3: Comece o seu trabalho**

Abra os arquivos `.ipynb` do projeto em seu ambiente Jupyter e execute as células para ver o código em ação. No seu notebook, carregue a chave do arquivo `.env` usando uma biblioteca como `python-dotenv` para acessá-la de forma segura.

---

### Próximos Passos (Concluído)

* [x] Explorar as funcionalidades da API;
* [x] Gerar um mapa mostrando os pontos de partida e destino;
* [x] Gerar um documento com o mapa e as informações de distância e duração das rotas;
* [ ] Postar informações (Endpoints de Otimização e Matriz);
* [ ] Obter informações a partir de um Endereço (Geocodificação);
* [ ] Descobrir o Endereço de um ponto (Geocodificação Reversa).