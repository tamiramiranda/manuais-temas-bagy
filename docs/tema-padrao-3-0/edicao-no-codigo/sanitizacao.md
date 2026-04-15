# Sanitização

O editor aplica **sanitização na colagem** (e, em alguns campos, também durante a edição) nos componentes `InputText`, `TextArea`, `RichText` e `Code`. O conteúdo que não for permitido é removido ou bloqueado; quando isso ocorre, o usuário recebe uma mensagem informativa. \
Abaixo veremos mais detalhes.

### Objetivo

Reduzir o risco de **XSS (Cross-Site Scripting)** e de **CSS malicioso** quando o lojista cola conteúdo nos campos do editor do tema. \
O fluxo principal é interceptar o evento de colagem e tratar o texto/HTML/CSS . Quando algo é removido ou bloqueado, o usuário vê uma mensagem informativa.

Esta camada no **frontend** oferece feedback imediato, reduz carga no servidor e evita erros antes do envio. O **back-end** mantém validação própria, a sanitização do editor **não substitui** a segurança do servidor.

### Stack técnica

<table><thead>
<tr><th>Camada</th><th>Biblioteca</th><th>Função</th></tr>
</thead><tbody>
<tr><td>HTML</td><td><a href="https://github.com/cure53/DOMPurify" target="_blank">DOMPurify</a></td><td>Lista de tags e atributos por tipo de campo.</td></tr>
<tr><td>CSS</td><td><a href="https://postcss.org/" target="_blank">PostCSS</a></td><td>Remove declarações e at-rules consideradas perigosas.</td></tr>
</tbody></table>

***

Segue tabela com o que cada campo permite de Tags e Atributos:

### Tags

<table><thead>
<tr><th>Tags</th><th>Permitida em</th></tr>
</thead><tbody>
<tr><td>a</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>abbr</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>address</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>article</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>aside</td><td><code>Code</code></td></tr>
<tr><td>audio</td><td><code>Code</code></td></tr>
<tr><td>b</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>blockquote</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>br</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>button</td><td><code>Code</code></td></tr>
<tr><td>caption</td><td><code>Code</code></td></tr>
<tr><td>cite</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>code</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>col</td><td><code>Code</code></td></tr>
<tr><td>colgroup</td><td><code>Code</code></td></tr>
<tr><td>datalist</td><td><code>Code</code></td></tr>
<tr><td>dd</td><td><code>Code</code></td></tr>
<tr><td>del</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>details</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>div</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>dl</td><td><code>Code</code></td></tr>
<tr><td>dt</td><td><code>Code</code></td></tr>
<tr><td>em</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>figcaption</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>figure</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>footer</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>h1</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>h2</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>h3</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>h4</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>h5</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>h6</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>header</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>hr</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>i</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>img</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>label</td><td><code>Code</code></td></tr>
<tr><td>legend</td><td><code>Code</code></td></tr>
<tr><td>li</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>mark</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>menu</td><td><code>Code</code></td></tr>
<tr><td>nav</td><td><code>Code</code></td></tr>
<tr><td>ol</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>p</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>picture</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>pre</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>progress</td><td><code>Code</code></td></tr>
<tr><td>q</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>s</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>section</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>small</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>source</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>span</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>strong</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>sub</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>summary</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>sup</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>table</td><td><code>Code</code></td></tr>
<tr><td>tbody</td><td><code>Code</code></td></tr>
<tr><td>td</td><td><code>Code</code></td></tr>
<tr><td>tfoot</td><td><code>Code</code></td></tr>
<tr><td>th</td><td><code>Code</code></td></tr>
<tr><td>thead</td><td><code>Code</code></td></tr>
<tr><td>time</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>tr</td><td><code>Code</code></td></tr>
<tr><td>track</td><td><code>Code</code></td></tr>
<tr><td>u</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>ul</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>video</td><td><code>Code</code></td></tr>
</tbody></table>

### Atributos

::: info Atenção:
Alguns dos atributos listados não podem ser usados em todas as tags HTML listadas acimas. É dever do desenvolvedor saber quais atributos podem ser usados com quais tags.
:::

<table><thead>
<tr><th>Atributos</th><th>Permitido em</th></tr>
</thead><tbody>
<tr><td>abbr</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>accesskey</td><td><code>Code</code></td></tr>
<tr><td>alt</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>cellpadding</td><td><code>Code</code></td></tr>
<tr><td>cellspacing</td><td><code>Code</code></td></tr>
<tr><td>cite</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>class</td><td><code>InputText</code>, <code>TextArea</code>,<code>RichText</code>, <code>Code</code></td></tr>
<tr><td>clear</td><td><code>Code</code></td></tr>
<tr><td>code</td><td><code>Code</code></td></tr>
<tr><td>cols</td><td><code>Code</code></td></tr>
<tr><td>colspan</td><td><code>Code</code></td></tr>
<tr><td>compact</td><td><code>Code</code></td></tr>
<tr><td>controls</td><td><code>Code</code></td></tr>
<tr><td>controlslist</td><td><code>Code</code></td></tr>
<tr><td>crossorigin</td><td><code>Code</code></td></tr>
<tr><td>data</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>datetime</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>decoding</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>default</td><td><code>Code</code></td></tr>
<tr><td>direction</td><td><code>Code</code></td></tr>
<tr><td>disablepictureinpicture</td><td><code>Code</code></td></tr>
<tr><td>disableremoteplayback</td><td><code>Code</code></td></tr>
<tr><td>disallowdocumentaccess</td><td><code>Code</code></td></tr>
<tr><td>download</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>draggable</td><td><code>Code</code></td></tr>
<tr><td>elementtiming</td><td><code>Code</code></td></tr>
<tr><td>end</td><td><code>Code</code></td></tr>
<tr><td>face</td><td><code>Code</code></td></tr>
<tr><td>headers</td><td><code>Code</code></td></tr>
<tr><td>height</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>high</td><td><code>Code</code></td></tr>
<tr><td>href</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>hreflang</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>hreftranslate</td><td><code>Code</code></td></tr>
<tr><td>hspace</td><td><code>Code</code></td></tr>
<tr><td>id</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>imagesizes</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>imagesrcset</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>importance</td><td><code>Code</code></td></tr>
<tr><td>incremental</td><td><code>Code</code></td></tr>
<tr><td>inert</td><td><code>Code</code></td></tr>
<tr><td>kind</td><td><code>Code</code></td></tr>
<tr><td>label</td><td><code>Code</code></td></tr>
<tr><td>lang</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>latencyhint</td><td><code>Code</code></td></tr>
<tr><td>leftmargin</td><td><code>Code</code></td></tr>
<tr><td>link</td><td><code>Code</code></td></tr>
<tr><td>loading</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>longdesc</td><td><code>Code</code></td></tr>
<tr><td>loop</td><td><code>Code</code></td></tr>
<tr><td>low</td><td><code>Code</code></td></tr>
<tr><td>lowsrc</td><td><code>Code</code></td></tr>
<tr><td>marginheight</td><td><code>Code</code></td></tr>
<tr><td>marginwidth</td><td><code>Code</code></td></tr>
<tr><td>media</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>muted</td><td><code>Code</code></td></tr>
<tr><td>nohref</td><td><code>Code</code></td></tr>
<tr><td>noresize</td><td><code>Code</code></td></tr>
<tr><td>noshade</td><td><code>Code</code></td></tr>
<tr><td>nowrap</td><td><code>Code</code></td></tr>
<tr><td>open</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>optimum</td><td><code>Code</code></td></tr>
<tr><td>playsinline</td><td><code>Code</code></td></tr>
<tr><td>poster</td><td><code>Code</code></td></tr>
<tr><td>pseudo</td><td><code>Code</code></td></tr>
<tr><td>referrerpolicy</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>rel</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>resources</td><td><code>Code</code></td></tr>
<tr><td>reversed</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>role</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>rows</td><td><code>Code</code></td></tr>
<tr><td>rowspan</td><td><code>Code</code></td></tr>
<tr><td>rules</td><td><code>Code</code></td></tr>
<tr><td>scope</td><td><code>Code</code></td></tr>
<tr><td>scrollamount</td><td><code>Code</code></td></tr>
<tr><td>scrolldelay</td><td><code>Code</code></td></tr>
<tr><td>scrolling</td><td><code>Code</code></td></tr>
<tr><td>sizes</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>span</td><td><code>Code</code></td></tr>
<tr><td>spellcheck</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>src</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>srclang</td><td><code>Code</code></td></tr>
<tr><td>srcset</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>standby</td><td><code>Code</code></td></tr>
<tr><td>start</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>step</td><td><code>Code</code></td></tr>
<tr><td>tabindex</td><td><code>Code</code></td></tr>
<tr><td>target</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>text</td><td><code>Code</code></td></tr>
<tr><td>title</td><td><code>InputText</code>, <code>TextArea</code>, <code>RichText</code>, <code>Code</code></td></tr>
<tr><td>topmargin</td><td><code>Code</code></td></tr>
<tr><td>translate</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>truespeed</td><td><code>Code</code></td></tr>
<tr><td>valuetype</td><td><code>Code</code></td></tr>
<tr><td>vspace</td><td><code>Code</code></td></tr>
<tr><td>width</td><td><code>RichText</code>, <code>Code</code></td></tr>
<tr><td>wrap</td><td><code>Code</code></td></tr>
</tbody></table>

***

### Camada CSS

Usada quando o conteúdo colado é identificado como CSS.

### Propriedades CSS Bloqueadas: `deniedProps`

<table><thead>
<tr><th>Propriedade</th><th>Razão</th></tr>
</thead><tbody>
<tr><td><code>behavior</code></td><td>Permite executar HTC scripts no IE</td></tr>
<tr><td><code>-moz-binding</code></td><td>XBL binding pode executar JS no Firefox antigo</td></tr>
<tr><td><code>expression</code></td><td>CSS expressions executam JS no IE</td></tr>
<tr><td><code>-ms-filter</code></td><td>Filtros IE podem conter código</td></tr>
<tr><td><code>filter</code></td><td>Pode conter expressions no IE</td></tr>
<tr><td><code>-o-link</code></td><td>Opera pode seguir links arbitrários</td></tr>
<tr><td><code>-o-link-source</code></td><td>Fonte de link no Opera</td></tr>
</tbody></table>

### Padrões de Valores Bloqueados: `deniedValues`

<table><thead>
<tr><th>Propriedade</th><th>Razão</th></tr>
</thead><tbody>
<tr><td><code>javascript:</code></td><td>Execução de JavaScript via URL</td></tr>
<tr><td><code>vbscript:</code></td><td>Execução de VBScript via URL</td></tr>
<tr><td><code>data:</code></td><td>Data URIs podem conter scripts</td></tr>
<tr><td><code>expression(</code></td><td>CSS expressions (IE)</td></tr>
<tr><td><code>url(javascript:)</code></td><td>JS em propriedades url()</td></tr>
<tr><td><code>@import</code></td><td>Pode carregar CSS externo malicioso</td></tr>
<tr><td><code>\\00</code></td><td>Caracteres escapados para bypass</td></tr>
</tbody></table>

Antes da análise principal, o editor remove linhas perigosas do tipo `@import` e `@charset`. Assim o CSS fica mais seguro e não quebra casos em que `@import` aparece só como texto dentro de uma propriedade.

No resultado final, podem faltar blocos vazios e as linhas podem ser reorganizadas, isso é esperado e não indica problema de segurança.

***

### Mensagens ao usuário

- Bloqueio total: _"O código colado não pôde ser mantido por motivos de segurança. Verifique o manual do tema para saber mais."_

- Remoção parcial: _"Parte do texto colado foi removido por motivos de segurança. Verifique o manual do tema para saber mais."_