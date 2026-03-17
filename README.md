# WordPress-Anti-Spam-Guide
🛡️ WordPress Anti-Spam Guide

Este guia prático foi criado para administradores de sites WordPress que enfrentam ataques massivos de bots e comentários de spam. Siga estas etapas para limpar seu banco de dados e blindar o site de novos ataques.

🚀 1. Limpeza Rápida (Bulk Actions)
Se o volume de spam for pequeno (centenas), use a interface nativa:

Vá em Comentários > Pendentes.

Clique em Opções de Tela (topo direito) e mude para 100 ou 200 itens por página.

Marque a caixa "Selecionar Todos".

Em Ações em Massa, escolha Mover para o lixo.

🐘 2. Limpeza Profunda (via SQL / phpMyAdmin)
Se o site tiver milhares de comentários, o WordPress pode travar. Use estes comandos SQL no seu banco de dados para uma limpeza instantânea:

⚠️ Atenção: Faça um backup do banco de dados antes de executar.

SQL
-- Apagar todos os comentários que aguardam aprovação
DELETE FROM wp_comments WHERE comment_approved = '0';

-- Apagar comentários marcados como SPAM
DELETE FROM wp_comments WHERE comment_approved = 'spam';

-- Limpar metadados órfãos (otimização após a limpeza)
DELETE FROM wp_commentmeta WHERE comment_id NOT IN (SELECT comment_ID FROM wp_comments);
Nota: Se o seu prefixo de tabela não for wp_, ajuste para o seu (ex: wp74_comments).

🛠️ 3. Configurações de Blindagem Nativa
No painel, vá em Configurações > Discussão e aplique estas travas:

Moderação Estratégica
Restrição de Links: Mude para 1 o valor de "Reter um comentário na fila se este contiver X ou mais links".

Comentários antigos: Ative "Encerrar automaticamente comentários em posts com mais de 30 dias".

Identificação: Marque "O autor do comentário tem que preencher o nome e e-mail".

Lista Negra de Palavras (Blacklist)
No campo "Comentários não permitidos", cole a lista abaixo (uma por linha, sem vírgulas). Isso moverá o comentário diretamente para a lixeira:

Plaintext
http://
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
🔌 4. Plugins Recomendados
Para uma solução "instale e esqueça":

Antispam Bee: Gratuito, cumpre a LGPD e não usa CAPTCHA chato.

Akismet: O padrão da indústria (requer chave API).

Disable Comments: Use se o site do seu cliente for institucional e não precisar de seção de comentários.

📝 Contribuição
Sinta-se à vontade para enviar um Pull Request com novos termos para a blacklist ou dicas de segurança para WordPress.

Guia criado para proteção de sites de clientes e otimização de performance.
