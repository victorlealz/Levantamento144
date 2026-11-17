# Levantamento144 v2.0

Atualização do aplicativo original, com a estrutura principal preservada.

## Publicação

1. Faça uma cópia de segurança do seu repositório e dos dados do navegador. Os registros locais existentes não são incluídos no ZIP.
2. Extraia o conteúdo do arquivo ZIP **diretamente na raiz do repositório**: os arquivos estão na raiz do ZIP e devem substituir os equivalentes antigos.
3. GitHub Pages: configure a implantação a partir da raiz do ramo que contém `index.html`. `index.html` é o único arquivo HTML do pacote. Atualize eventuais links que utilizavam o nome HTML antigo.
4. Cloudflare Workers: a implantação original via `wrangler.toml` e `worker.js` continua disponível. O worker também serve `ui.css`, `qr-local.js`, `logo.png` e `favicon.png`.
5. Abra o aplicativo, confira os QR Codes e teste a impressão A4 usando "Salvar como PDF", com as configurações padrão de margens do navegador (CSS `@page`).

## O que mudou

- QR Codes vetoriais em SVG, sem CDN: 108 × 108 px na tela e 128 × 128 px no PDF. No celular muito estreito, a prévia se adapta a 90 px; o PDF mantém 128 px.
- Fotografias de alvo com upload: 96 × 96 px na tela e 108 × 108 px na impressão. Sem upload, placeholder de 48 × 48 px na tela e 54 × 54 px na impressão.
- Imagem do local/endereço no painel 02, antes da validação: JPG, PNG ou WebP (até 20 MB), com pré-visualização, remoção e largura regulável de 80 a 186 mm (170 mm por padrão), aplicada ao PDF A4. A imagem integra o backup local.
- O botão de localizar Hospital/UPA e Delegacia foi deslocado para abaixo dos dois quadros e centralizado; nos celulares, ocupa a largura do painel.
- O botão "Gerar Relatório" está centralizado, com acabamento azul translúcido (glassmorphism), bordas arredondadas e responsividade preservada.
- Removidos os painéis de visão geral e avisos, os avisos do PDF e os textos de orientação/legendas explicativas na tela e no relatório. Rótulos dos campos e placeholders foram mantidos.
- Geração de PDF por impressão A4, com paginação automática e sem limite fixo. Assinatura única imediatamente antes do footer final.
- Marca e favicon oriundos do ícone fornecido; paleta neutra e caixas de cantos retos.
- Validação geográfica em duas etapas: coordenadas preenchidas/verificadas e confirmação explícita do responsável. Endereço não conferido é apresentado como não verificado.
- Os três índices têm controles deslizantes de 0 a 100%, iniciando em 50%, sem campo numérico manual. A alteração atualiza imediatamente os indicadores e o relatório. Os percentuais são estimativas informadas pelo usuário.
- Registro de classificação, fonte e data para endereço, presença e avaliação de risco. A validação e as mensagens de erro permanecem; os avisos não bloqueiam a emissão.
- Validação de CPF, confirmação antes da limpeza e consultas usando o CPF atualizado. Os cálculos de completude e pendências foram preservados internamente, sem os painéis visuais removidos.
- Salvamento de campos no `localStorage` e de fotos no `IndexedDB`, exportação/importação local de backup JSON. Falhas de quota não substituem os dados por um registro incompleto.

## Privacidade e limites

- Não há backend nem upload automático de CPFs, fotos ou relatórios. Os dados permanecem no navegador utilizado. **O armazenamento local não está criptografado por este aplicativo**; evite equipamentos compartilhados e mantenha cópias de segurança protegidas.
- Os dados são processados localmente, mas o botão para localizar unidades usa serviços públicos externos de geocodificação (Nominatim/OSM e Overpass), enviando o endereço consultado. O clique nos links de mapa envia o endereço/coordenadas ao provedor do mapa. Essas consultas são opcionais; o formulário e o PDF funcionam sem elas.
- Não confunda coordenadas sugeridas pelo mapa com localização confirmada. A marcação "Confirmado" requer conferência manual.
- Se a versão anterior foi utilizada, dados preservados podem conter valores inicialmente presumidos. Ao migrar o rascunho legado, opções anteriormente pré-selecionadas passam a "Não avaliado".
- A gravação local pode falhar em modo privado, em browsers com armazenamento restrito ou após limpeza dos dados do site. Em caso de alerta de armazenamento cheio, exporte imediatamente um backup JSON.
- Os arquivos JSON exportados contêm dados pessoais, incluindo fotografias, em texto legível (base64 para as fotos). Trate-os como documentos confidenciais.
- Este aplicativo é um instrumento de registro, não uma fonte autônoma de verificação de fatos ou uma ferramenta de decisão operacional automatizada.

## Arquivos principais

- `index.html`: único arquivo HTML, ponto de entrada para GitHub Pages.
- `worker.js`, `wrangler.toml`: implantação via Cloudflare Worker.
- `ui.css`: CSS local, inclusive estilos de impressão.
- `qr-local.js`: gerador de QR Codes local, com licenças em `LICENSE-QR.txt`.
- `logo.png`, `favicon.png`: identidade visual anexada.
