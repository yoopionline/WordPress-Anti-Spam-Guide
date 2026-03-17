# 🛡️ Guia Anti-Spam para WordPress

Este repositório contém um guia prático e configurações prontas para limpar e blindar sites WordPress contra ataques massivos de robôs e comentários de spam.

---

## 🚀 1. Limpeza em Massa (Interface WP)

Se o volume de spam for moderado, use as **Ações em Massa** nativas:

1. Acesse **Comentários > Pendentes**.
2. No topo direito, clique em **Opções de Tela**.
3. Altere o "Número de itens por página" para `100` ou `200`.
4. Marque a caixa de seleção global (ao lado de 'Autor').
5. No menu **Ações em Massa**, selecione **Mover para o Lixo** e clique em **Aplicar**.

---

## 🐘 2. Limpeza Profunda (via SQL / phpMyAdmin)

Para sites com milhares de comentários travando o painel, execute estes comandos no **SQL** do seu banco de dados:

> **⚠️ IMPORTANTE:** Faça um backup do banco de dados antes de executar.

```sql
-- Apagar todos os comentários pendentes de uma vez
DELETE FROM wp_comments WHERE comment_approved = '0';

-- Apagar comentários marcados como SPAM
DELETE FROM wp_comments WHERE comment_approved = 'spam';

-- Limpar metadados órfãos (otimização após a limpeza)
DELETE FROM wp_commentmeta WHERE comment_id NOT IN (SELECT comment_ID FROM wp_comments);

Nota: Se o prefixo das suas tabelas não for wp_, ajuste o comando (ex: wp74_comments).

## 🛡️ 3. Configuração de Blindagem NativaAcesse Configurações > Discussão no painel administrativo e aplique os seguintes ajustes para reduzir drasticamente o trabalho manual:ConfiguraçãoAção NecessáriaMotivoModeração de LinksAlterar para 1Bots raramente comentam sem incluir um link.Fechamento AutomáticoAtivar para 30 diasEvita ataques em posts antigos que não estão sob vigilância.ObrigatoriedadeMarcar "Nome e E-mail"Cria uma barreira básica contra scripts simples.Aprovação ManualManter Sempre AtivoGarante que nenhum spam apareça publicamente.

## 🚫 4. Blacklist de Termos ProibidosO campo "Comentários não permitidos" é a sua ferramenta mais poderosa. Qualquer comentário que contenha um dos termos abaixo será movido diretamente para a lixeira, poupando sua fila de moderação.[!IMPORTANT]Regra de Ouro: Cole uma palavra por linha. Não use vírgulas ou outros separadores.Lista para Copiar e Colar:Plaintexthttp://

https://
.ru
.top
.xyz
.click
.link
.pw
viagra
cialis
casino
poker
betting
slot
blackjack
crypto
bitcoin
ethereum
investment
profit
earn money
make money
work from home
whatsapp +
wa.me
telegram.me
t.me
cheap price
discount
free gift
essay help
write my paper

##🔌 5. Plugins RecomendadosPara uma camada de inteligência extra (filtro de comportamento e banco de dados global de spam):Antispam Bee: 🏆 Melhor escolha. Gratuito, extremamente leve e totalmente em conformidade com a LGPD/GDPR (não envia dados para servidores externos).Akismet Anti-Spam: A solução oficial da Automattic. Muito robusta, mas exige chave API e é paga para sites comerciais.Disable Comments: A solução radical. Se o site do cliente não precisa de interação, use este plugin para remover completamente o sistema de comentários do banco de dados.

📝 Mantido por: https://github.com/yoopionline

🤝 Contribuições: Sinta-se à vontade para abrir um Pull Request com novos termos para a lista de bloqueio.
