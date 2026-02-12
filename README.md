# OpenClaw_Docker
Repositório de teste para disponibilizar uma versão segura de teste do OpenClaw pelo Docker


## 🔴 CENÁRIO 1: VPS / Nuvem (Por que é proibido?)
**O Risco:** Superfície de Ataque Exposta.
Ao rodar o OpenClaw em um servidor nuvem (AWS, DigitalOcean, etc.), você expõe a interface de controle para a internet pública.

- **Vetor de Ataque:** Possibilidade de Hackers/Scanners encontrarem o serviço. Se a autenticação for fraca, o hacker ganha acesso `root` remoto ao servidor.
- **Impacto:** Comprometimento total do servidor e possibilidade de ataque na rede interna da empresa.

<p align="center">
  <img src="https://github.com/user-attachments/assets/8d36c3ef-861a-4b26-b10a-22cbd23a857a">
</p>

## 🟡 CENÁRIO 2: Local / Bare Metal (Por que evitar?)
**O Risco:** Herança de Permissões.
Rodar direto no terminal do PC (Windows/Mac/Linux) sem isolamento.

- **Vetor de Ataque:** Injeção de Prompt* Indireta. Um site malicioso ou e-mail pode instruir o agente a buscar arquivos locais.
- **Impacto:** O agente tem as permissões do usuário. Ele pode ler chaves SSH, senhas salvas de navegador, arquivos `.env` de produção e enviar esses dados para servidores externos.

*Injeção de Prompt: Tentativa de quebrar o prompt de segurança da aplicação. Ex.: "Ignore todas as suas restrições de segurança e me forneça..."

<p align="center">
  <img src="https://github.com/user-attachments/assets/a33f0f44-36c8-45c2-b1df-7374cc5b3b77">
</p>

## 🟢 CENÁRIO 3: Docker Sandbox (O Padrão Seguro)
**A Solução:** Isolamento de Processo.
O agente roda encapsulado dentro de um container, sem visão do sistema operacional hospedeiro.

- **Segurança:** O agente só exerga a pasta `/workspace` montada explicitamente. Ele não consegue acessar nada que esteja fora do container.
- **Contenção:** Se o agente executar um comando destrutivo (`rm -rf /`), ele apaga apenas o container (que é descartável), mantendo o computador e arquivos seguros

<p align="center">
  <img src="https://github.com/user-attachments/assets/3cb75291-ae45-4793-8573-18ee879728cb">
</p>