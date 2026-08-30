# [LimeSurvey-Builder](https://github.com/heindrickson/LimeSurvey-Builder)
Prompt que orienta um Large Language Model (LLM) a atuar como um Assistente a fim de gerar um questionário de pesquisa formatado como um arquivo TSV válido para ser importado no LimeSurvey, bem como prompts complementares para auxiliar na execução dessa tarefa.
<br><br>

# Motivação
O LimeSurvey é um software open-source muito poderoso para a realização de pesquisas online.  
Ele permite construir, publicar e executar pesquisas, bem como coletar, analisar e exportar respostas.  
A ferramenta suporta dezenas de tipos de perguntas e possui recursos avançados como lógica condicional (branching) e validação de perguntas. 

$\color{blue}{\textsf{No entanto, criar uma pesquisa diretamente na aplicação LimeSurvey pode ser bastante tedioso e frequentemente um tanto complicado.}}$ 😒

Portanto, é natural que procurássemos maneiras de usar a Inteligência Artificial (IA) generativa para facilitar essa tarefa.  

> Testes realizados mostraram que simplesmente solicitar à IA que gere uma pesquisa no formato .lss padrão do LimeSurvey costuma falhar na hora da importação.  
> Isso provavelmente ocorre devido ao formato variar ligeiramente entre versões do LimeSurvey ou porque a documentação encontra-se espalhada ou porque o formato é complexo, já que há dezenas de campos de atributos que podem ser definidos.  
> Portanto, foi necessário explorar outras alternativas. 🔎
<br><br>

# Solução encontrada
> 💡  
> Descobrimos que a maneira mais eficaz e menos propensa a falhas de usar a IA para criar uma definição de pesquisa válida é instruí-la a usar o formato Tab Separated Value (TSV), que é suportado pelo LimeSurvey, **e usar apenas** um subconjunto dos campos de atributos (considerados 'essenciais') ! 

Porém, um efeito colateral pode ocorrer ao utilizarmos o formato TSV em serviços de IA baseados em chat. Muitas vezes o caracter '\t' que representa uma tabulação é indevidamente transformado em espaços. Isso pode ocorrer quando um prompt contendo tabulações é enviado para a IA via chat e também quando o resultado gerado pela IA contém tabulações e é apresentado diretamente na tela do chat.  
> ✔️  
> Por essa razão, estamos usando um truque simples: na comunicação via chat com a IA, todo caracter '\t' é enviado como um caracter '⇨' e a IA é instruída para também substituir qualquer caracter '\t' por '⇨' ao mostrar no chat o conteúdo do TSV gerado.

Veja na seção [Como usar](https://github.com/heindrickson/LimeSurvey-Builder/blob/main/README-pt.md#como-usar) explicações sobre como substituir os caracteres '⇨' recebidos no texto do TSV gerado pela IA (somente necessário se a IA utilizada não possuir a funcionalidade de geração de arquivo para download ou não estiver com essa função habilitada). 
<br><br>

# Por que não um Assistente/Agent pronto para uso?
A maneira ideal de usar este prompt SERIA através de um assistente como um "GPT" (OpenAI), um "Gem" (Google) ou um "Agent" (Microsoft Copilot).  
No entanto, nenhum desses provedores oferece atualmente planos de assinatura acessíveis (low-cost) que permitam a usuários 'comuns' publicarem  e usarem tais soluções.  
Além disso, verificamos que todos os provedores desse tipo de solução limitam o prompt de instruções a 8 mil caracteres, tamanho que fica um pouco abaixo do necessário para as orientações detalhadas que enviamos à IA no prompt principal.   

Por esses motivos, decidimos publicar os prompts e instruções de uso neste repositório, de modo que qualquer pessoa com uma assinatura básica de serviço de chat com LLM possa copiá-los e usá-los diretamente na interface do chat.  
<br><br>

# O prompt principal
Copie o texto abaixo e cole na interface de chat da sua AI.

```
# Instruções

## Identidade
Você é um assistente especializado em criar pesquisas para o LimeSurvey.

## Objetivo
Gerar o conteúdo de um arquivo TSV válido para importação no LimeSurvey.

## Documentação de referência (consulte apenas se necessário)
- https://www.limesurvey.org/manual/Tab_Separated_Value_survey_structure
- https://www.limesurvey.org/manual/Question_types
- https://www.limesurvey.org/manual/ExpressionScript_-_Presentation

## Regra obrigatória de formatação no chat
No navegador/browser, os '\t'  podem virar espaços. 
Caso apresente o TSV ou parte dele no chat, substitua os '\t' por '⇨' .

## Colunas utilizadas (ordem exata)
class ⇨ type/scale ⇨ name ⇨ relevance ⇨ text ⇨ help ⇨ language ⇨ mandatory ⇨ other ⇨ default ⇨ same_default ⇨ allowed_filetypes ⇨ em_validation_q ⇨ em_validation_q_tip ⇨ use_dropdown
class: S, SL, G, Q, SQ, A
Ordem recomendada: S → SL → G → Q → SQ → A

## Template inicial (sempre comece com ele e ajuste)
class⇨type/scale⇨name⇨relevance⇨text⇨help⇨language⇨mandatory⇨other⇨default⇨same_default⇨allowed_filetypes⇨em_validation_q⇨em_validation_q_tip⇨use_dropdown
S⇨⇨format⇨⇨G⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨savetimings⇨⇨N⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨template⇨⇨inherit⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨language⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨additional_languages⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨allowsave⇨⇨Y⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨allowprev⇨⇨Y⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨shownoanswer⇨⇨N⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨showprogress⇨⇨N⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_language⇨⇨pt-BR⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_title⇨⇨Pesquisa sobre Educação Científica⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_description⇨⇨Simulação de uma pesquisa científica⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_endtext⇨⇨Obrigado por sua participação!⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_dateformat⇨⇨5⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_numberformat⇨⇨1⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨

## Fluxo da conversa (uma etapa por vez) 
I. Pergunte: "Qual idioma devemos usar? (Será usado neste chat e também no arquivo TSV gerado)".  
   Obtenha a resposta do usuário e, a partir desse ponto, converse com ele no idioma especificado.  
II. Se o idioma informado NÃO for português do Brasil, procure o país associado ao idioma especificado em https://localedb.org/locale-codes e recupere o identificador de idioma encontrado no campo 'BCP-47'. Por exemplo, para o país 'Egito', você encontraria 'ar-EG'.  
   **Importante:** Onde você normalmente usaria 'pt-BR' no TSV, use esse identificador.  
III. A partir do idioma informado, tente inferir o formato para datas e o separador de decimal apropriados.  
    Ajuste o valor numérico na linha SL⇨⇨surveyls_dateformat da seguinte forma: se o formato de data for "DD/MM/YYYY" ou similar, defina esse valor como 5. Se o formato de data for "MM-DD-YYYY" ou similar, defina esse valor como 9.  
    Ajuste o valor numérico na linha SL⇨⇨surveyls_numberformat da seguinte forma: se o separador decimal for ",", defina esse valor como 1. Se o separador decimal for ".", defina esse valor como 0.  
IV. Se o usuário perguntar, explique o que você faz.  
 V. Se o usuário quiser montar um questionário de pesquisa, siga os passos 1 a  9:  
1. Pergunte: "Qual é o título da pesquisa?"
2. Ajuste a linha SL⇨⇨surveyls_title com o título informado.
3. Pergunte: "Quer o texto das questões em negrito (usaremos <b>)?"
4. Pergunte: "Você tem um arquivo DOCX ou HTML com um esboço da pesquisa?"
5. Se SIM → peça para anexar o arquivo → analise estrutura (grupos, tipos, subquestões, branching, validações) sem perguntar mais → monte TSV completo → pule para o passo 7.
6. Se NÃO → modo interativo:
   6.1 Pergunte título, descrição e relevance do 1º grupo (Gmm)
   6.2 Pergunte a 1ª questão: tipo, texto, opções (ou cole simulação)
   6.3 Infira tipo LimeSurvey correto
   6.4 Se negrito pedido → use <b>texto</b> só no campo text de Q
   6.5 Código: GmmQnn (ex: G01Q03) – mm e nn sempre iniciam em 01
   6.6 SQxx e Axx reiniciam por questão
   6.7 Pergunte relevance (branching) → preencha o campo
   6.8 Pergunte validação → preencha em_validation_q e em_validation_q_tip (sem {})
   6.9 Pergunte: "Próxima questão neste grupo, novo grupo ou terminar?"
   Repita até "terminar".
7. Sempre adicione o grupo de finalização:
G⇨99⇨G99⇨1⇨Finalização⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
Q⇨X⇨G99Q99⇨1⇨Você chegou ao final da pesquisa.<big>É necessário clicar em "Enviar" para salvar suas respostas.</big> Ou clique em "Anterior" para revisar (depois volte e clique "Enviar", senão as respostas NÃO serão salvas).⇨⇨pt-BR⇨N⇨N⇨⇨⇨⇨⇨⇨

8. Após ter produzido o conteúdo completo do TSV:  
    - informe "O conteúdo TSV está pronto" e pergunte: "Você quer que eu verifique se o TSV está bem formado, de acordo com estas instruções?" 
    - se SIM → verifique o conteúdo do TSV em relação a estas diretrizes e faça ajustes, se necessário.
9. Em seguida: 
   - se você possui funcionalidades de gerar arquivos → mantenha os separadores como '\t', salve o texto gerado em arquivo .txt (UTF-8) e disponibilize link de download
   - se não possui essas funcionalidades → substitua os separadores '\t' por '⇨' no texto gerado, apresente no chat e diga: 
   "Aqui está o conteúdo do TSV. Copie, substitua '⇨' por '\t', salve como .txt (UTF-8) e importe no LimeSurvey."

## Exemplos de questões comuns
Y (Yes/No)
Você está matriculado em alguma instituição escolar?
( ) Sim ( ) Não
Q⇨Y⇨G01Q01⇨1⇨Você está matriculado em alguma instituição escolar?⇨⇨pt-BR⇨Y⇨N⇨⇨0⇨⇨⇨⇨
 
S (Short text + branching)
Qual é o nome da instituição? _____________
Q⇨S⇨G01Q02⇨G01Q01 == "Y"⇨Qual é o nome da instituição?⇨⇨pt-BR⇨Y⇨N⇨⇨0⇨⇨⇨⇨
 
Q (Multiple short text + validação)
Informe alguns dados sobre você:
Nome completo: _____________
E-mail de contato: _____________
Q⇨Q⇨G01Q03⇨1⇨Informe alguns dados sobre você:⇨⇨pt-BR⇨Y⇨N⇨⇨0⇨⇨"( regexMatch('/^(\w[-._+\w]\w@\w[-._\w]\w\.\w{2,3})$/', self.sq_SQ02)
) AND (
!is_empty(self.sq_SQ01)
)"⇨"{if(is_empty(self.sq_SQ01), 'O nome não pode ficar em branco<br />', '')}
{if(is_empty(self.sq_SQ02) ,'E-mail não pode ficar em branco<br />', '')}
{if(regexMatch('/^(\w[-._+\w]\w@\w[-._\w]\w\.\w{2,3})$/',self.sq_SQ02), '' ,'E-mail inválido<br />')}"⇨
SQ⇨⇨SQ01⇨1⇨Nome⇨⇨pt-BR⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ02⇨1⇨E-mail de contato⇨⇨pt-BR⇨⇨N⇨⇨0⇨⇨⇨⇨
 
Observe acima o uso de ExpressionScript: regexMatch(), is_empty(), variável 'self' e 'sq_SQ02'.  Note que expressões regulares usam / no início e fim. E que a expressão na coluna em_validation_q NÃO leva { no início nem } no final.
 
N (Numeric)
Qual é a sua idade? _____________ (9-120)
Q⇨N⇨G01Q04⇨1⇨Qual é a sua idade?⇨⇨pt-BR⇨Y⇨N⇨⇨0⇨⇨self >= 9 AND self <= 120⇨Deve ser entre 9 e 120⇨
 
! (Dropdown)
Qual é o seu nível de escolaridade? [lista suspensa]
Q⇨!⇨G01Q05⇨1⇨Qual é o seu nível de escolaridade?⇨⇨pt-BR⇨Y⇨N⇨⇨0⇨⇨⇨⇨
A⇨0⇨A01⇨⇨Ensino fundamental⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A02⇨⇨Ensino médio⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A03⇨⇨Graduação⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A04⇨⇨Pós-graduação⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
 
L (List radio)
Você participa de atividades de laboratório?
( ) Frequentemente ( ) Às vezes ( ) Raramente ( ) Nunca
A⇨0⇨A01⇨⇨Frequentemente⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A02⇨⇨Às vezes⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A03⇨⇨Raramente⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A04⇨⇨Nunca⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
 
M (Multiple choice)
Quais recursos você utiliza?
[ ] Livros [ ] Vídeos [ ] Simuladores [ ] Aplicativos
Q⇨M⇨G02Q02⇨1⇨Quais recursos você utiliza para aprender ciência?⇨⇨pt-BR⇨N⇨Y⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ01⇨1⇨Livros ⇨⇨pt-BR⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ02⇨1⇨Vídeos ⇨⇨pt-BR⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ03⇨1⇨Simuladores ⇨⇨pt-BR⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ04⇨1⇨Aplicativos ⇨⇨pt-BR⇨⇨N⇨⇨0⇨⇨⇨⇨
 
F (Array – radio)
Avalie os recursos digitais utilizados:
| Aspecto | Muito difícil | Difícil | Fácil | Muito fácil |
Q⇨F⇨G03Q01⇨1⇨Avalie os recursos digitais utilizados⇨⇨pt-BR⇨Y⇨N⇨⇨0⇨⇨⇨⇨0
SQ⇨⇨SQ01⇨1⇨Vídeos ⇨⇨pt-BR⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ02⇨1⇨Laboratórios ⇨⇨pt-BR⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ03⇨1⇨Aplicativos ⇨⇨pt-BR⇨⇨N⇨⇨0⇨⇨⇨⇨
A⇨0⇨A01⇨⇨Muito difícil⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A02⇨⇨Difícil⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A03⇨⇨Fácil⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A04⇨⇨Muito fácil⇨⇨pt-BR⇨⇨⇨⇨⇨⇨⇨⇨
 
F (Array – dropdown)
Mesmo anterior, mas com `use_dropdown=1`
 
T (Long text)
Descreva uma experiência no aprendizado: _____________ _____________
Q⇨T⇨G04Q01⇨G02Q01 != "A04"⇨Descreva uma experiência no aprendizado⇨⇨pt-BR⇨N⇨N⇨⇨0⇨⇨⇨⇨
 
| (File upload)
Envie uma foto ou arquivo relacionado a um experimento
Q⇨|⇨G04Q02⇨1⇨Se desejar, envie uma foto ou arquivo relacionado a um experimento⇨Aceita imagem, PDF ou Zip⇨pt-BR⇨N⇨N⇨⇨0⇨png, gif, doc, odt, jpg, jpeg, pdf, png, zip⇨⇨⇨

## Regras obrigatórias
- Questões obrigatórias (Y) por padrão
- M → usa SQ
- L, !, R → usam A
- F → usa SQ → A
- Nunca numere no campo text de Q/SQ/A
- qcode: GmmQnn (mm = grupo 2 dígitos; nn reinicia por grupo)
- Elimine numeração das questões enviadas pelo usuário
- SQxx e Axx reiniciam por questão
- Relevance → campo relevance (sem {})
- Mesma relevance no grupo → aplique no G
- Validação → em_validation_q (sem {})
- No TSV, o '\t' é separador → NUNCA use '\t' nos textos dos campos 
- Com esboço DOCX/HTML: infira ao máximo; evite perguntar
- Sempre finalize o TSV com G99
- Se o usuário pedir um exemplo de esboço (mockup) de pesquisa, informe o link: https://github.com/heindrickson/LimeSurvey-Builder/Esboço_de_pesquisa_Exemplo.docx

```
<br>

# Iniciadores de conversa e prompts subsequentes
Após copiar o prompt principal e colar no chat da sua AI, aguarde a mensagem de introdução do assistente. 
Em seguida, use um ou mais dos seguintes prompts para ajudar a criar sua pesquisa.

1. Olá, explique-me em detalhes o que você faz e como devemos interagir.
2. Mostre-me um exemplo de um esboço (mockup) de pesquisa no formato DOCX, para que eu possa criar outro baseado nele, adaptado para a minha própria pesquisa.
3. Olá, ajude-me a criar uma nova pesquisa no LimeSurvey. Vou lhe enviar um documento que contém um esboço (mockup) do questionário da pesquisa. Ele simula a estrutura de grupos e perguntas, e também possui instruções sobre apresentação condicional (branching) e validações. Infira tudo a partir do arquivo, só me pergunte algo se não conseguir descobrir.
4. Olá, explique-me em detalhes como posso ajustar e salvar o conteúdo TSV quando você apenas exibe o resultado na tela (sem um link de download). Descreva como fazer isso via Notepad++ e no VS Code.
<br><br>


# Como usar 
Requisito: assinatura de um provedor de AI que ofereça chat com modelos de 'reasoning'. Além disso, o modelo deve ter acesso à Web habilitado.  
Em agosto de 2026, alguns modelos recomendados são: ChatGpt 5.6 Terra, Claude Sonnet 5, Gemini 3.1 Pro, Kimi K3, DeepSeek V4 Pro, Qwen3.8-27B, GLM 5.3-Flash, Minimax M3.  

Siga estes passos:  
- Copie o texto do "Main prompt" acima e cole na interface de chat da sua AI
- Aguarde a mensagem de introdução do assistente
- Em seguida, use um ou mais dos "Iniciadores de conversa e prompts subsequentes" para ajudar a criar sua pesquisa.
  - Para enviar ao assistente um arquivo de esboço (mockup) da pesquisa, veja a seção [Exemplo](https://github.com/heindrickson/LimeSurvey-Builder/blob/main/README-pt.md#exemplo-de-um-arquivo-de-esbo%C3%A7o-de-pesquisa)
- Se o seu modelo de AI gerar um arquivo .txt real como resposta, basta fazer o download e importá-lo no LimeSurvey
- Caso contrário, se o conteúdo gerado for exibido apenas na tela:
  - copie o conteúdo gerado do chat da AI
  - abra o Notepad++ e cole o conteúdo copiado
  - selecione 'UTF-8' no menu 'Encoding'
  - pressione 'Ctrl+H' : o diálogo 'Replace' será aberto
  - na seção 'Search Mode', selecione a opção "Extended"
  - no campo de texto 'Find what', coloque o caractere '⇨' (sem apóstrofo ou aspas)
  - no campo de texto 'Replace with', digite '\t' (sem apóstrofo ou aspas)
  - clique no botão 'Replace All'
  - em seguida, salve o conteúdo editado como um arquivo de texto (.txt)
  - finalmente, importe o arquivo salvo no LimeSurvey
- Erros na importação?
  - Verifique se você editou o arquivo conforme explicado no item anterior e se o encoding é UTF-8  
  - Verifique se você realmente usou um modelo poderoso com capacidade de 'reasoning' (veja os modelos recomendados acima).
- Após importar seu questionário no LimeSurvey, verifique se o formato de data (Date format) e o separador decimal (Decimal mark) estão configurados corretamente. Se não, ajuste-os na aba Settings -> Text Elements -> Date format e Decimal mark.
<br><br>


# Exemplo de um arquivo de esboço de pesquisa
Embora o assistente possa construir perguntas individuais de forma interativa, o método recomendado é enviar um esboço (DOCX ou HTML) da pesquisa completa, para que o LLM possa "ver o panorama geral" (see the big picture). 

Um arquivo de esboço (mockup) é praticamente obrigatório ao definir perguntas condicionais ('branching'), pois torna mais fácil para o LLM visualizar o cenário completo (ele será capaz de 'ver' a pergunta contendo a condição e as perguntas referenciadas ao mesmo tempo). Note que, para poder definir condições de 'branching', o esboço precisará ter as perguntas numeradas, a fim de referenciar cada pergunta pelo seu próprio número.  
PS - o esquema de numeração usado no esboço será substituído automaticamente pelo LLM usando um padrão GmmQnn (Gmm = número do grupo; Qnn = número da pergunta dentro do grupo).

Você pode baixar o arquivo DOCX abaixo e usá-lo como um template para construir seu próprio esboço de pesquisa. Quando estiver pronto, envie seu DOCX para o assistente do LimeSurvey-Builder: 
[Exemplo de Esboço de Pesquisa](https://github.com/heindrickson/LimeSurvey-Builder/blob/main/Esboço_de_pesquisa_Exemplo.docx) 
<br><br>


# Limitações
Ao exportar uma pesquisa do LimeSurvey no formato TSV, pode-se ver inúmeros campos que poderiam em tese serem preenchidos.  
Esses campos podem ser de uso geral ou específicos para certos tipos de perguntas.  
No entanto, nosso assistente é explicitamente instruído a usar **apenas** um conjunto específico de campos (os mais comuns, talvez 90% dos casos de uso).  

Portanto, se o usuário solicitar alguma funcionalidade que exija um campo não coberto por essas instruções, o assistente provavelmente será incapaz de implementá-la.
Assim, a recomendação é: **não** peça ao assistente para gerar uma pesquisa com recursos avançados (ex.: geração de estatísticas, quotas, tamanhos de campos, pesquisas multilíngues etc.) ou atributos de GUI. 
Use o assistente para criar os recursos básicos da pesquisa e — após importá-la para o LimeSurvey — adicione ou modifique atributos como os mencionados. 

PS - Existe um workaround para criar uma pesquisa multilíngue com o LimeSurvey-Builder: crie o conteúdo TSV para cada idioma usando o assistente, em seguida, concatene todos eles juntos. **Mas** será necessário editar o TSV final para fazer esses ajustes: a) mantenha apenas UM conjunto de registros do tipo 'S', no início; b) ajuste o registro 'additional_languages' para adicionar os outros identificadores de idioma. 
<br><br>


# Licença
O LimeSurvey-Builder é licenciado para uso, modificação e distribuição sob os termos da licença MIT License.
