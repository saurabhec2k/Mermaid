```mermaid
graph LR
    %% Local Environment
    subgraph Local Environment
        A[streamlit_app/]
        A1[main.py]
        A2[llm_bot.py]
        A3[config.yml]
        subgraph Artifacts
            A4[Dockerfile]
            A5[environment.yml]
        end
    end

    %% Docker Environment
    subgraph Docker Environment
        D1["docker build -t bot:v1 ."]
        D2["docker run --rm -p 8000:8000 bot:v1"]
    end

    %% Azure Deployment
    subgraph Azure Deployment
        AD1[Azure Web App]
        AD2[Azure Container Registry]
        AD3[Azure CLI]
        subgraph ACR Commands
            AD3A["az acr create"]
            AD3B["az acr build"]
        end
        subgraph Web App Commands
            AD3C["az webapp create"]
            AD3D["az webapp config appsettings set"]
        end
    end

    %% Azure OpenAI/ACS Integration
    subgraph Azure OpenAI/ACS Integration
        AO1[Azure OpenAI]
        AO2[Azure Cognitive Search]
    end

    %% Logging and Troubleshooting
    subgraph Logging and Troubleshooting
        L1["az webapp log stream"]
        L2[Azure Portal]
    end

    %% Connections and Interactions
    A -->|Run Locally| D1
    A -->|Build Docker| AD2
    AD2 -->|Push Container| AD1
    AD3A --> AD2
    AD3B --> AD2
    AD3C --> AD1
    AD3D --> AD1
    AD1 --> AO1
    AD1 --> AO2
    AD1 --> L1
    AD1 --> L2
    D1 -->|Run Container| D2
