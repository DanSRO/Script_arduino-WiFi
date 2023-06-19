# Script_arduino-WiFi
Passo a passo conexão wifi e envio SMTP em ARDUINO  


1. Instalar biblioteca ESP32 e biblioteca SMTP.
2. Conectar ESP32 ao Wi-Fi utilizando a biblioteca WiFi do Arduino. O ESP32 conectado à mesma rede Wi-Fi que o servidor SMTP.
3. Criar conexão SMTP com o servidor SMTP utilizando a biblioteca SMTP do Arduino.
4. Autenticar conexão SMTP com o servidor SMTP. Geralmente com um nome de usuário e senha.
5. Criar mensagem de e-mail com a biblioteca SMTP do Arduino. Incluir remetente, destinatário, assunto e corpo da mensagem.
6. Enviar mensagem de e-mail usando conexão SMTP.


#include <WiFi.h>
#include <SMTPClient.h>

// Configurações da rede Wi-Fi
const char* ssid = "NOME_DA_REDE_WIFI";
const char* password = "SENHA_DA_REDE_WIFI";

// Configurações do servidor SMTP
const char* smtp_server = "SERVIDOR_SMTP";
const int smtp_port = 587;
const char* smtp_user = "USUARIO_SMTP";
const char* smtp_password = "SENHA_SMTP";

void setup() {
  // Conecta-se à rede Wi-Fi
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Conectando-se à rede Wi-Fi...");
  }
  Serial.println("Conexão Wi-Fi estabelecida.");

  // Configura a conexão SMTP
  SMTPClient smtp;
  smtp.setRemote(smtp_server, smtp_port);
  smtp.setLogin(smtp_user, smtp_password);

  // Cria uma mensagem de e-mail
  smtp.beginMessage("remetente@dominio.com", "destinatario@dominio.com", "Assunto do e-mail");
  smtp.println("Corpo da mensagem do e-mail.");
  smtp.endMessage();

  // Envia a mensagem de e-mail
  if (smtp.send() == 1) {
    Serial.println("E-mail enviado com sucesso.");
  } else {
    Serial.println("Falha ao enviar e-mail.");
  }
}

void loop() {
  // Nada aqui.
}

Substituir configurações da rede Wi-Fi, do servidor SMTP, do usuário e da senha. A biblioteca SMTPClient do Arduino é de terceiros, portanto, precisará instalá-la manualmente.
