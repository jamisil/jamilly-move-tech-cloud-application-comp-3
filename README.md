# Move Tech Cloud Application


Este repositório contém o projeto prático desenvolvido durante o curso **Move Tech** (Magalu e Prósper Digital Skills) - Formação em Cloud Computing para iniciantes.

**Desenvolvido por:** Jamilly Venâncio Da Silva

---

## Sobre o Projeto

Trata-se de uma API simples de micro e-commerce com gerenciamento de pedidos e itens, construída em Python utilizando o framework FastAPI.

Atualmente, a aplicação armazena os dados em memória. O objetivo principal desta competência é preparar a infraestrutura e realizar o deploy automatizado da aplicação na nuvem.

### Endpoints Disponíveis

| Método   | Rota                   | Descrição                       |
| :------- | :--------------------- | :------------------------------ |
| `GET`    | `/health`              | Verifica se a API está no ar    |
| `POST`   | `/orders`              | Cria um novo pedido             |
| `GET`    | `/orders`              | Lista todos os pedidos          |
| `GET`    | `/orders/{id}`         | Retorna um pedido com seus itens|
| `DELETE` | `/orders/{id}`         | Cancela um pedido               |
| `POST`   | `/orders/{id}/items`   | Adiciona um item ao pedido      |
| `GET`    | `/orders/{id}/items`   | Lista os itens de um pedido     |

---

## Objetivos da Competência 3

Ao final desta etapa, a aplicação deverá estar **versionada, conteinerizada e publicada na Magalu Cloud**. O checklist de entregas inclui:

- [X] Publicar a imagem no Container Registry da Magalu Cloud
- [X] Criar o manifest Kubernetes (`k8s/app.yaml`)
- [X] Realizar o deploy no cluster Kubernetes da Magalu Cloud
- [X] Configurar o pipeline de CI/CD no GitHub Actions

---

## Configuração do Docker

O repositório inclui um arquivo `Dockerfile` configurado para empacotar a aplicação em uma imagem Docker otimizada:

```dockerfile
FROM python:3.11-slim          # Imagem base com Python 3.11

WORKDIR /app                   # Diretório de trabalho dentro do container

RUN pip install poetry==1.8.3  # Instala o gerenciador de dependências

COPY pyproject.toml poetry.lock* ./
RUN poetry config virtualenvs.create false && \
    poetry install --without dev --no-root  # Instala apenas as dependências de produção

COPY app/ ./app/               # Copia o código da aplicação

EXPOSE 8000                    # Porta que a aplicação vai escutar

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
