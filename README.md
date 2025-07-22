# 📬 Serviço de Notificação por E-mail

Microserviço simples em **Spring Boot** que só faz uma coisa: **envia e-mails**.

## 🚀 O que ele faz

- Envia e-mails personalizados usando templates HTML via **Thymeleaf**.

## 🧩 Tecnologias usadas

- **Spring Boot Starter Mail** – envio de e-mail.  
- **Spring Boot Starter Thymeleaf** – templates HTML.  
- **Spring Boot Starter Web** – API REST.  
- **Lombok** – redução de boilerplate.

```

## 📫 Endpoint para enviar e-mail

**POST** `/email`

### Exemplo de JSON que o endpoint recebe:

```json
{
  "id": "123",
  "nomeTarefa": "Finalizar Projeto",
  "descricao": "Terminar a documentação e enviar para o cliente.",
  "dataCriacao": "22-07-2025 15:30:00",
  "dataEvento": "23-07-2025 09:00:00",
  "emailUsuario": "destinatario@email.com",
  "dataAlteracao": "22-07-2025 18:00:00",
  "statusNotificacaoEnum": "PENDENTE"
}
```

## 🧪 Testando no Postman

- Método: `POST`  
- URL: `http://localhost:8085/email`  
- Headers:  
  - `Content-Type: application/json`  
- Body:  
  - Raw JSON (igual o exemplo aí em cima)

## 🧾 Template de e-mail (notificacao.html)

Coloca esse arquivo em `src/main/resources/templates/notificacao.html`:

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Notificação de Tarefa</title>
</head>
<body>
    <h2>Olá!</h2>
    <p>Você tem uma nova tarefa agendada:</p>
    <ul>
        <li><strong>Nome:</strong> <span th:text="${nomeTarefa}">NOME</span></li>
        <li><strong>Data do Evento:</strong> <span th:text="${dataEvento}">DATA</span></li>
        <li><strong>Descrição:</strong> <span th:text="${descricao}">DESCRIÇÃO</span></li>
    </ul>
    <p>Não se esqueça! ;)</p>
</body>
</html>
```

## ⚙️ Configuração no application.yml

```yaml
spring:
  mail:
    host: smtp.gmail.com
    port: 587
    username: # seu email aqui
    password: # sua senha aqui
    protocol: smtp
    properties:
      mail:
        smtp:
          socketFactory:
            port: 465
            class: javax.net.ssl.SSLSocketFactory
            fallback: false
          auth: true
          starttls:
            enable: true
          connectiontimeout: 5000
          timeout: 3000
          writetimeout: 5000

  thymeleaf:
    enable: true

envio:
  email:
    remetente: # seu email aqui
    nomeRemetente: # seu nome aqui

server:
  port: 8085
```

---

👤 Feito por Kaio Cesar
