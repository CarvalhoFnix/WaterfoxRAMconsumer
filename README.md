## Waterfox e o consumo de RAM

Data: 26/09/2026 - Hora aproximada no Brasil -> 07:20.

# Problema
- Durante uma verificação no Gerenciador de tarefas, foi constatado o uso excessivo de RAM do navegador Waterfox, chegando a marca de quase 5GB. 

- Ao analisar o mesmo, o PID 7699 estava consumo aproximadamente 1.5GB de RAM.

# PID: 7699 - Waterfox bin o que esse binário faz?

O waterfox-bin (ou o executável waterfox / waterfox.bin) é o núcleo, o arquivo executável principal do navegador Waterfox.   

- Em termos diretos: é ele quem faz o navegador rodar de fato.   

- Quando você vê esse processo rodando no seu gerenciador de tarefas (como o Gerenciador de Tarefas do Windows ou o monitor do Linux), ele representa o motor do navegador em funcionamento, gerenciando a interface, as abas, os scripts e o processamento das páginas web que você visita.

# Por que ele estava consumindo tanta RAM (quase 5 GB)?

- O processo principal do navegador: gerencia perfis, histórico e extensões.   

-  Processos filhos (conteúdo/abas): cada aba aberta, principalmente sites pesados (como redes sociais com rolagem infinita, painéis em tempo real, editores online ou vídeos em alta resolução), abre uma instância própria vinculada a esse binário para isolar as páginas e evitar que o navegador inteiro feche se uma aba travar.

- Se o consumo disparou para 5 GB, significa que o waterfox-bin acumulou muitas abas ativas em segundo plano sem liberá-las, ou sofreu algum memory leak (vazamento de memória) pontual em alguma extensão ou site específico.

# Solução

1 - Extensão: Auto Tab Discard
- Para que serve: Ela "congela" (descarta) automaticamente as abas que ficam ociosas por um tempo determinado, liberando a RAM que elas estavam usando. Quando você clica na aba de novo, ela recarrega na hora.

- Configurações essenciais que foram realizadas:
  - Tempo de inatividade: Definido para 15 ou 30 minutos (para a aba não dormir rápido demais se você só tirar o olho dela por um instante).
  - Símbolo visual: Marcado para aparecer um ícone (como um emoji 💤) nas abas congeladas, facilitando a identificação.
  -  Proteções inteligentes: Foi configurado para nunca descartar abas que estão tocando mídia (como YouTube/Spotify), abas fixadas (como o WhatsApp Web) ou abas onde você está digitando formulários.
  -  Exceções: Você pode usar o menu da extensão para proteger sites que não quer que durmam de jeito nenhum.

2 - Resumo das Configurações do Navegador (Waterfox / Gecko)

- Como o motor baseado no Firefox tende a isolar muito os processos (o famigerado `waterfox-bin`), algumas medidas ajudam a conter o consumo geral:
  
- Gerenciador de Processos Interno: Use o comando `about:processes` na barra de endereços para monitorar qual aba ou extensão está sugando mais memória em tempo real.
- Limpeza de Cache sob demanda: Se notar o consumo subindo sem motivo, digite `about:memory` e clique em Minimize memory usage para forçar o navegador a esvaziar a RAM ociosa.
- Ajuste de Processos (`about:config`): Se quiser ir além, você pode procurar pelo parâmetro `dom.ipc.processCount` e diminuir o número de processos paralelos que o navegador cria para as abas, reduzindo o uso geral de memória em PCs mais modestos.

# Resultado
- Após as configurações, o consumo reduziu para uma média de 1.5GB e 1.70GB com 5 abas abertas contínuas.
- PID 7699: Consumo reduzido para uma média 400MB a 500MB.

# Isenção de responsabilidade
- O uso de IA e extensões ficará seu critério. Use-as com responsabilidade e sempre verifique extensões que desconhece, leiam a documentação da extensão sempre que possível. A análise de processos é recomendado que faça de forma isolada, de preferência em máquina virtual, caso queira fazer em sua máquina principal, não coloque seus dados, faça com o navegador "puro".

# Contribuidores adicionas: Gemini


