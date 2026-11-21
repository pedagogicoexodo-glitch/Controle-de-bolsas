[Controle de Bolsas.html](https://github.com/user-attachments/files/35211302/Controle.de.Bolsas.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Colégio Êxodo — Controle de Bolsas e Parceiros</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        iframe#netlify-badge, div#netlify-badge, a[href*="netlify.com/prod"], div:has(> a[href*="netlify.com"]), .netlify-badge {
            display: none !important;
            visibility: hidden !important;
            opacity: 0 !important;
            pointer-events: none !important;
            z-index: -999999 !important;
        }

        @media print {
            body * {
                visibility: hidden;
            }
            #secaoRelatorioGeral, #secaoRelatorioGeral * {
                visibility: visible;
            }
            #secaoRelatorioGeral {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
                background: white !important;
                padding: 0 !important;
                margin: 0 !important;
                box-shadow: none !important;
                border: none !important;
            }
            #secaoRelatorioGeral button, #secaoRelatorioGeral select {
                display: none !important;
            }
        }
    </style>
</head>
<body class="bg-gradient-to-b from-purple-950 via-purple-900/5 to-slate-100 min-h-screen text-slate-800 font-sans antialiased" onload="inicializarSistema()">

    <!-- TELA DE LOGIN -->
    <div id="telaLogin" class="fixed inset-0 bg-gradient-to-tr from-slate-950 via-purple-950 to-indigo-900 flex items-center justify-center p-4 z-50">
        <div class="bg-white w-full max-w-md rounded-3xl shadow-2xl p-8 space-y-6 border border-purple-100/20 backdrop-blur-lg">
            <div class="text-center space-y-3">
                <div class="inline-flex items-center justify-center p-4 bg-purple-50/50 rounded-2xl mb-1 shadow-inner border border-purple-100">
                    <img src="https://lh3.googleusercontent.com/d/1OsUAwEW_R2bBJUTb3YRkpFXJs1Xy84Xb=w800" alt="Colégio Êxodo" class="h-20 w-auto object-contain">
                </div>
            </div>

            <form onsubmit="fazerLogin(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-600 uppercase mb-1.5 tracking-wider">Usuário</label>
                    <input type="text" id="loginUsuario" required placeholder="Digite seu usuário..." class="w-full px-4 py-3 border border-slate-200 rounded-2xl text-sm outline-none focus:ring-2 focus:ring-purple-700 bg-slate-50/50 transition">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 uppercase mb-1.5 tracking-wider">Senha</label>
                    <input type="password" id="loginSenha" required placeholder="••••••••" class="w-full px-4 py-3 border border-slate-200 rounded-2xl text-sm outline-none focus:ring-2 focus:ring-purple-700 bg-slate-50/50 transition">
                </div>
                <button type="submit" class="w-full bg-purple-900 hover:bg-purple-800 text-white font-semibold py-3.5 rounded-2xl transition shadow-lg shadow-purple-900/20 text-sm">Entrar no Sistema</button>
            </form>
        </div>
    </div>

    <!-- APLICAÇÃO PRINCIPAL -->
    <div id="appPrincipal" class="hidden min-h-screen flex flex-col">
        <header class="bg-white/95 backdrop-blur-md text-purple-950 shadow-sm relative z-10 border-b border-purple-100">
            <div class="max-w-7xl mx-auto px-6 py-4 flex flex-col md:flex-row justify-between items-center gap-3">
                <div class="flex items-center gap-3.5">
                    <div class="bg-white px-3.5 py-2 rounded-2xl shadow-sm flex items-center justify-center border border-purple-100">
                        <img src="https://lh3.googleusercontent.com/d/1OsUAwEW_R2bBJUTb3YRkpFXJs1Xy84Xb=w800" alt="Colégio Êxodo" class="h-10 w-auto object-contain">
                    </div>
                    <div>
                        <h1 class="text-xl font-bold tracking-wide text-purple-900">COLÉGIO ÊXODO</h1>
                        <p class="text-[11px] text-slate-500 font-medium">Plataforma de Gestão de Bolsas e Parceiros</p>
                    </div>
                </div>
                <div class="flex items-center gap-2.5 flex-wrap justify-end">
                    <span id="sync-status" class="text-xs bg-yellow-600 text-white px-3.5 py-1.5 rounded-full font-semibold shadow-sm">Sincronizando...</span>
                    <div class="bg-purple-50/80 px-3.5 py-1.5 rounded-xl text-xs border border-purple-200/60 flex items-center gap-2 shadow-sm">
                        <span class="text-slate-500 font-medium">Logado:</span>
                        <span id="labelPerfilLogado" class="font-bold text-purple-900 uppercase">--</span>
                    </div>
                    <button onclick="abrirConfiguracoes()" id="btnMenuConfig" class="bg-purple-100/70 hover:bg-purple-200 text-purple-900 text-xs font-semibold px-3.5 py-2 rounded-xl transition border border-purple-200/60 hidden shadow-sm">⚙️ Configurações</button>
                    <button onclick="fazerLogout()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold px-3.5 py-2 rounded-xl transition border border-purple-200/60 shadow-sm">🚪 Sair</button>
                </div>
            </div>
        </header>

        <main class="max-w-7xl mx-auto px-6 py-6 space-y-6 flex-1 w-full">
            
            <!-- PAINEL DO PARCEIRO (TELA CHEIA EXCLUSIVA) -->
            <div id="painelParceiroTelaCheia" class="hidden space-y-6">
                <div class="bg-white/95 backdrop-blur-sm p-6 rounded-3xl shadow-sm border border-slate-200/80 space-y-6">
                    <div class="flex justify-between items-center border-b pb-4">
                        <div>
                            <h2 class="text-xl font-bold text-purple-900" id="tituloPainelParceiroFull">Painel do Parceiro</h2>
                            <p class="text-xs text-slate-500 mt-0.5">Visualize seus lotes de bolsas adquiridas e faça o acompanhamento dos alunos.</p>
                        </div>
                        <button onclick="gerarRelatorioParceiroPorNome(window.parceiroLogadoNome)" class="bg-purple-900 hover:bg-purple-800 text-white text-xs font-semibold px-4 py-2.5 rounded-xl transition shadow-sm">📄 Relatório Detalhado</button>
                    </div>

                    <div class="space-y-4" id="blocoHistoricoLotesParceiroFull">
                        <h4 class="font-bold text-slate-700 text-sm">📦 Histórico de Lotes Registrados</h4>
                        <div class="border border-slate-200/80 rounded-2xl overflow-hidden bg-white shadow-sm">
                            <table class="w-full text-left text-xs">
                                <thead class="bg-slate-100/70 text-slate-600 border-b border-slate-200">
                                    <tr>
                                        <th class="p-3.5">Data</th>
                                        <th class="p-3.5">Qtd Bolsas</th>
                                        <th class="p-3.5">Modalidade</th>
                                        <th class="p-3.5">Valor Total</th>
                                        <th class="p-3.5">Status Financeiro</th>
                                    </tr>
                                </thead>
                                <tbody id="tabelaHistoricoLotesParceiroFull" class="divide-y divide-slate-100"></tbody>
                            </table>
                        </div>
                    </div>

                    <div class="space-y-4 pt-2">
                        <h4 class="font-bold text-slate-700 text-sm">Bolsas Adquiridas e Controle de Certificação</h4>
                        <div class="border border-slate-200/80 rounded-2xl overflow-hidden shadow-sm bg-white">
                            <table class="w-full text-left text-sm">
                                <thead class="bg-slate-50 text-xs uppercase text-slate-500 border-b border-slate-200">
                                    <tr>
                                        <th class="p-3.5">Bolsa</th>
                                        <th class="p-3.5">Modalidade</th>
                                        <th class="p-3.5">Status</th>
                                        <th class="p-3.5">Aluno Vinculado</th>
                                        <th class="p-3.5 text-right">Certificação</th>
                                    </tr>
                                </thead>
                                <tbody id="tabelaVagasParceiroFull" class="divide-y divide-slate-100"></tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <!-- VISÃO GERAL (ADMIN / FUNCIONÁRIO) -->
            <div id="painelVisaoGeral" class="space-y-6">
                <!-- CARDS DE AÇÃO RÁPIDA -->
                <div class="grid grid-cols-1 md:grid-cols-4 gap-4" id="cardsAcaoRapida">
                    <button onclick="verificarPermissaoMaster(abrirModalCadastroParceiro)" class="bg-gradient-to-br from-white via-white to-purple-50/40 p-5 rounded-3xl shadow-sm border border-slate-200/80 hover:border-purple-800 hover:shadow-lg transition flex items-center gap-3.5 text-left group">
                        <div class="p-3.5 bg-purple-100 text-purple-900 group-hover:bg-purple-900 group-hover:text-white rounded-2xl text-lg transition shadow-sm">➕</div>
                        <div>
                            <h3 class="font-bold text-slate-800 text-xs group-hover:text-purple-900 transition">Novo Parceiro</h3>
                            <p class="text-[11px] text-slate-500 mt-0.5">Cadastrar nova empresa</p>
                        </div>
                    </button>

                    <button onclick="voltarPainelPrincipal()" class="bg-gradient-to-br from-white via-white to-purple-50/40 p-5 rounded-3xl shadow-sm border border-slate-200/80 hover:border-purple-800 hover:shadow-lg transition flex items-center gap-3.5 text-left group">
                        <div class="p-3.5 bg-purple-100 text-purple-900 group-hover:bg-purple-900 group-hover:text-white rounded-2xl text-lg transition shadow-sm">🤝</div>
                        <div>
                            <h3 class="font-bold text-slate-800 text-xs group-hover:text-purple-900 transition">Gerenciar Parceiros</h3>
                            <p class="text-[11px] text-slate-500 mt-0.5">Listagem e tabelas</p>
                        </div>
                    </button>

                    <button onclick="verificarPermissaoMaster(abrirPaginaRegistrarCompra)" class="bg-gradient-to-br from-white via-white to-purple-50/40 p-5 rounded-3xl shadow-sm border border-slate-200/80 hover:border-purple-800 hover:shadow-lg transition flex items-center gap-3.5 text-left group">
                        <div class="p-3.5 bg-purple-100 text-purple-900 group-hover:bg-purple-900 group-hover:text-white rounded-2xl text-lg transition shadow-sm">📦</div>
                        <div>
                            <h3 class="font-bold text-slate-800 text-xs group-hover:text-purple-900 transition">Registrar Compra</h3>
                            <p class="text-[11px] text-slate-500 mt-0.5">Adicionar lote de bolsas</p>
                        </div>
                    </button>

                    <button onclick="abrirPaginaRelatorioGeral()" class="bg-gradient-to-br from-white via-white to-purple-50/40 p-5 rounded-3xl shadow-sm border border-slate-200/80 hover:border-purple-800 hover:shadow-lg transition flex items-center gap-3.5 text-left group">
                        <div class="p-3.5 bg-purple-100 text-purple-900 group-hover:bg-purple-900 group-hover:text-white rounded-2xl text-lg transition shadow-sm">📊</div>
                        <div>
                            <h3 class="font-bold text-slate-800 text-xs group-hover:text-purple-900 transition">Relatório Geral</h3>
                            <p class="text-[11px] text-slate-500 mt-0.5">Consolidado e detalhes</p>
                        </div>
                    </button>
                </div>

                <!-- PAINEL GERENCIAR PARCEIROS -->
                <div id="secaoGerenciarParceiros" class="bg-white/95 backdrop-blur-sm p-6 rounded-3xl shadow-sm border border-slate-200/80 space-y-6">
                    <div class="flex flex-col md:flex-row justify-between items-center border-b border-slate-100 pb-4 gap-4">
                        <div>
                            <h2 class="text-lg font-bold text-slate-800" id="tituloSecaoGerenciar">🤝 Gerenciar Parceiros</h2>
                            <p class="text-xs text-slate-500 mt-0.5" id="subtituloSecaoGerenciar">Gerencie empresas e pesquise rapidamente.</p>
                        </div>
                        <div class="flex items-center gap-2 w-full md:w-auto" id="containerBuscaParceiro">
                            <input type="text" id="inputBuscaParceiro" oninput="atualizarInterface();" placeholder="Pesquisar parceiro..." class="px-4 py-2.5 border border-slate-200 rounded-2xl text-sm outline-none bg-slate-50/50 w-full md:w-64">
                        </div>
                    </div>

                    <div class="border border-slate-200/80 rounded-2xl overflow-hidden shadow-sm bg-white">
                        <table class="w-full text-left text-sm">
                            <thead class="bg-slate-50 text-xs uppercase text-slate-500 border-b border-slate-200" id="cabecalhoTabelaParceiros">
                                <tr>
                                    <th class="p-4">Empresa / Parceiro</th>
                                    <th class="p-4">Documento (CNPJ/CPF)</th>
                                    <th class="p-4">Contato</th>
                                    <th class="p-4 text-center">Bolsas Contratadas</th>
                                    <th class="p-4 text-center">Status de Ocupação</th>
                                    <th class="p-4 text-right">Ações</th>
                                </tr>
                            </thead>
                            <tbody id="tabelaParceirosLista" class="divide-y divide-slate-100"></tbody>
                        </table>
                    </div>
                </div>

                <!-- REGISTRAR COMPRA -->
                <div id="secaoRegistrarCompra" class="bg-white/95 backdrop-blur-sm p-8 rounded-3xl shadow-sm border border-slate-200/80 hidden space-y-6">
                    <div class="flex justify-between items-center border-b pb-4">
                        <h2 class="text-xl font-bold text-purple-900">📦 Registrar Nova Compra de Bolsas</h2>
                        <button onclick="voltarPainelPrincipal()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold px-4 py-2 rounded-xl">⬅️ Voltar</button>
                    </div>
                    <form id="formCompra" onsubmit="registrarCompraLocal(event)" class="grid grid-cols-1 md:grid-cols-2 gap-5">
                        <div>
                            <label class="block text-xs font-bold text-slate-600 uppercase mb-1.5">Selecione o Parceiro Oficial</label>
                            <select id="selectParceiroCompra" required class="w-full px-4 py-3 border border-slate-200 rounded-2xl bg-slate-50 text-sm"></select>
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-600 uppercase mb-1.5">Quantidade de Bolsas</label>
                            <input type="number" id="qtdBolsas" required min="1" value="1" oninput="atualizarCalculoAutomatico()" class="w-full px-4 py-3 border border-slate-200 rounded-2xl bg-slate-50 text-sm" placeholder="Ex: 10">
                        </div>
                        
                        <div class="md:col-span-2 bg-purple-50/50 p-4 rounded-2xl border border-purple-100 space-y-3">
                            <label class="flex items-center gap-2 cursor-pointer">
                                <input type="checkbox" id="checkAuto" onchange="toggleCalculoAuto()" class="w-4 h-4 text-purple-900 rounded border-slate-300 focus:ring-purple-700">
                                <span class="text-xs font-bold text-purple-900 uppercase">Informar Valor Unitário por Bolsa (Calcular Automaticamente o Total)</span>
                            </label>
                            <div id="blocoValorUnitario" class="hidden">
                                <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Valor Unitário por Bolsa (R$)</label>
                                <input type="number" step="0.01" id="valorUnitario" oninput="atualizarCalculoAutomatico()" class="w-full px-4 py-3 border border-slate-200 rounded-2xl bg-white text-sm" placeholder="Ex: 150,00">
                            </div>
                        </div>

                        <div>
                            <label class="block text-xs font-bold text-slate-600 uppercase mb-1.5">Valor Total (R$)</label>
                            <input type="text" id="valorTotal" required class="w-full px-4 py-3 border border-slate-200 rounded-2xl bg-slate-50 text-sm font-bold text-purple-900" placeholder="Ex: 3000,00">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-600 uppercase mb-1.5">Status Financeiro</label>
                            <select id="statusFinanceiro" class="w-full px-4 py-3 border border-slate-200 rounded-2xl bg-slate-50 text-sm">
                                <option value="PAGO">Pago</option>
                                <option value="PENDENTE">Pendente</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-600 uppercase mb-1.5">Modalidade / Tipo de Bolsa</label>
                            <select id="modalidade" class="w-full px-4 py-3 border border-slate-200 rounded-2xl bg-slate-50 text-sm">
                                <option value="EJA">EJA</option>
                                <option value="TÉCNICO">TÉCNICO</option>
                                <option value="TÉCNICO - AGRO">TÉCNICO - AGRO</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-600 uppercase mb-1.5">Data da Compra</label>
                            <input type="date" id="dataCompra" required class="w-full px-4 py-3 border border-slate-200 rounded-2xl bg-slate-50 text-sm">
                        </div>
                        <div class="md:col-span-2">
                            <label class="block text-xs font-bold text-slate-600 uppercase mb-1.5">Observações</label>
                            <textarea id="observacoesCompra" rows="2" class="w-full px-4 py-3 border border-slate-200 rounded-2xl bg-slate-50 text-sm" placeholder="Detalhes adicionais..."></textarea>
                        </div>
                        <div class="md:col-span-2 pt-2">
                            <button type="submit" id="btnSalvarCompra" class="w-full bg-purple-900 hover:bg-purple-800 text-white font-semibold py-4 rounded-2xl shadow-lg">Registrar Compra e Gerar Bolsas</button>
                        </div>
                    </form>
                </div>

                <!-- RELATÓRIO GERAL -->
                <div id="secaoRelatorioGeral" class="bg-white/95 backdrop-blur-sm p-8 rounded-3xl shadow-sm border border-slate-200/80 hidden space-y-6">
                    <div class="flex flex-col md:flex-row justify-between items-center border-b pb-4 gap-4">
                        <div>
                            <h2 class="text-xl font-bold text-purple-900">📊 Relatório Executivo e Consolidado da Escola</h2>
                            <p class="text-xs text-slate-500 mt-0.5">Visão completa financeira, de lotes e do andamento pedagógico.</p>
                        </div>
                        <div class="flex gap-2 flex-wrap">
                            <select id="filtroModalidadeRelatorio" onchange="abrirPaginaRelatorioGeral()" class="px-4 py-2 border border-slate-200 rounded-xl text-xs bg-slate-50 font-medium">
                                <option value="TODAS">Todas as Modalidades</option>
                                <option value="EJA">EJA</option>
                                <option value="TÉCNICO">TÉCNICO</option>
                                <option value="TÉCNICO - AGRO">TÉCNICO - AGRO</option>
                            </select>
                            <button onclick="baixarPlanilhaRelatorio()" class="bg-emerald-700 hover:bg-emerald-800 text-white text-xs font-semibold px-4 py-2 rounded-xl shadow-sm">📥 Baixar Planilha (CSV)</button>
                            <button onclick="window.print()" class="bg-purple-900 hover:bg-purple-800 text-white text-xs font-semibold px-4 py-2 rounded-xl shadow-sm">🖨️ Imprimir</button>
                            <button onclick="voltarPainelPrincipal()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold px-4 py-2 rounded-xl">⬅️ Voltar</button>
                        </div>
                    </div>
                    <div id="conteudoRelatorioGeralPagina" class="space-y-6"></div>
                </div>
            </div>
        </main>
    </div>

    <!-- MODAL CONFIGURAÇÕES (GESTÃO DE USUÁRIOS E ACESSOS) -->
    <div id="modalConfig" class="fixed inset-0 bg-black/60 backdrop-blur-sm hidden flex items-center justify-center p-4 z-50">
        <div class="bg-white w-full max-w-2xl rounded-3xl shadow-2xl p-6 space-y-5">
            <div class="flex justify-between items-center border-b pb-3">
                <h3 class="font-bold text-lg text-purple-900" id="tituloModalConfig">⚙️ Gestão de Usuários e Acessos</h3>
                <button onclick="fecharConfiguracoes()" class="font-bold text-lg">✕</button>
            </div>
            
            <div class="space-y-4">
                <form onsubmit="salvarUsuarioSistema(event)" id="formUsuarioConfig" class="bg-purple-50/50 p-4 rounded-2xl border border-purple-100 grid grid-cols-1 md:grid-cols-3 gap-3 items-end">
                    <input type="hidden" id="editIndexUsuario" value="-1">
                    <div>
                        <label class="block text-[11px] font-bold text-slate-600 uppercase mb-1">Usuário</label>
                        <input type="text" id="novoUsuarioLogin" required placeholder="Ex: recepcao" class="w-full px-3 py-2 border rounded-xl bg-white text-xs">
                    </div>
                    <div>
                        <label class="block text-[11px] font-bold text-slate-600 uppercase mb-1">Senha</label>
                        <input type="text" id="novoUsuarioSenha" required placeholder="••••••" class="w-full px-3 py-2 border rounded-xl bg-white text-xs">
                    </div>
                    <div>
                        <label class="block text-[11px] font-bold text-slate-600 uppercase mb-1">Perfil</label>
                        <select id="novoUsuarioPerfil" onchange="toggleSelectEmpresaConfig()" class="w-full px-3 py-2 border rounded-xl bg-white text-xs">
                            <option value="funcionario">Funcionário</option>
                            <option value="master">Administrador (Master)</option>
                            <option value="parceiro">Parceiro</option>
                        </select>
                    </div>
                    <div class="md:col-span-2" id="blocoSelectEmpresaConfig">
                        <label class="block text-[11px] font-bold text-slate-600 uppercase mb-1">Empresa Vinculada</label>
                        <select id="novoUsuarioEmpresaSelect" class="w-full px-3 py-2 border rounded-xl bg-white text-xs"></select>
                    </div>
                    <div class="md:col-span-1 flex gap-2">
                        <button type="submit" id="btnSalvarUsuarioConfig" class="flex-1 bg-purple-900 hover:bg-purple-800 text-white font-semibold py-2 rounded-xl text-xs">Adicionar</button>
                        <button type="button" onclick="cancelarEdicaoUsuario()" id="btnCancelarUsuarioConfig" class="hidden px-3 bg-slate-200 text-slate-700 font-semibold py-2 rounded-xl text-xs">Cancelar</button>
                    </div>
                </form>

                <div class="overflow-x-auto border rounded-2xl">
                    <table class="w-full text-left text-xs">
                        <thead class="bg-slate-50 uppercase text-slate-500 border-b">
                            <tr>
                                <th class="p-3">Usuário</th>
                                <th class="p-3">Perfil</th>
                                <th class="p-3">Empresa Vinculada</th>
                                <th class="p-3 text-right">Ação</th>
                            </tr>
                        </thead>
                        <tbody id="tabelaUsuariosConfig" class="divide-y divide-slate-100"></tbody>
                    </table>
                </div>
            </div>

            <div class="flex justify-end pt-2 border-t">
                <button onclick="fecharConfiguracoes()" class="bg-slate-200 text-slate-700 font-semibold px-5 py-2 rounded-xl text-xs">Fechar</button>
            </div>
        </div>
    </div>

    <!-- MODAL CADASTRO PARCEIRO -->
    <div id="modalCadastrarParceiro" class="fixed inset-0 bg-black/60 backdrop-blur-sm hidden flex items-center justify-center p-4 z-50">
        <div class="bg-white w-full max-w-md rounded-3xl shadow-2xl p-6 space-y-4">
            <h3 class="font-bold text-lg text-purple-900">Cadastrar Novo Parceiro</h3>
            <form onsubmit="salvarNovoParceiro(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Nome / Razão Social</label>
                    <input type="text" id="nomeNovoParceiro" required class="w-full px-4 py-3 border border-slate-200 rounded-2xl uppercase text-sm">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 uppercase mb-1">CNPJ/CPF</label>
                    <input type="text" id="documentoParceiro" placeholder="Opcional" class="w-full px-4 py-3 border border-slate-200 rounded-2xl text-sm">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Contato</label>
                    <input type="text" id="contatoParceiro" placeholder="Telefone" class="w-full px-4 py-3 border border-slate-200 rounded-2xl text-sm">
                </div>
                <div class="flex gap-2">
                    <button type="submit" class="flex-1 bg-purple-900 text-white font-semibold py-3 rounded-2xl">Cadastrar</button>
                    <button type="button" onclick="fecharModalCadastroParceiro()" class="px-4 bg-slate-200 rounded-2xl">Cancelar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL DETALHES PARCEIRO (ADMIN / FUNCIONÁRIO) -->
    <div id="modalParceiro" class="fixed inset-0 bg-black/60 backdrop-blur-sm hidden flex items-center justify-center p-4 z-50">
        <div class="bg-white w-full max-w-6xl rounded-3xl shadow-2xl overflow-hidden max-h-[90vh] flex flex-col">
            <div class="bg-purple-900 text-white p-5 flex justify-between items-center">
                <h3 class="font-bold text-lg" id="modalTituloParceiro">Painel do Parceiro</h3>
                <div class="flex items-center gap-2">
                    <button onclick="gerarRelatorioParceiro()" class="bg-purple-800 hover:bg-purple-700 text-white text-xs font-semibold px-3.5 py-2 rounded-xl transition shadow-sm">📄 Relatório</button>
                    <button onclick="fecharModal()" class="text-white font-bold text-lg">✕</button>
                </div>
            </div>
            <input type="hidden" id="editParceiroAtualModal">
            <div class="p-6 overflow-y-auto space-y-6 flex-1">
                <div class="bg-slate-50/80 p-5 rounded-2xl border border-slate-200/80 space-y-3" id="blocoHistoricoLotesModal">
                    <h4 class="font-bold text-slate-700 text-sm">📦 Histórico de Lotes Registrados</h4>
                    <div class="border border-slate-200/80 rounded-2xl overflow-hidden bg-white shadow-sm">
                        <table class="w-full text-left text-xs">
                            <thead class="bg-slate-100/70 text-slate-600 border-b border-slate-200">
                                <tr>
                                    <th class="p-3.5">Data</th>
                                    <th class="p-3.5">Qtd Bolsas</th>
                                    <th class="p-3.5">Modalidade</th>
                                    <th class="p-3.5" id="thValorLoteModal">Valor Total</th>
                                    <th class="p-3.5">Status Financeiro</th>
                                    <th class="p-3.5">Lançado por</th>
                                    <th class="p-3.5 text-right">Ação</th>
                                </tr>
                            </thead>
                            <tbody id="tabelaHistoricoLotesModal" class="divide-y divide-slate-100"></tbody>
                        </table>
                    </div>
                </div>

                <div>
                    <h4 class="font-semibold text-slate-700 mb-3 text-sm">Bolsas Adquiridas e Controle de Certificação</h4>
                    <div class="border border-slate-200/80 rounded-2xl overflow-hidden shadow-sm">
                        <table class="w-full text-left text-sm">
                            <thead class="bg-slate-50 text-xs uppercase text-slate-500 border-b border-slate-200">
                                <tr>
                                    <th class="p-3.5">Bolsa</th>
                                    <th class="p-3.5">Modalidade</th>
                                    <th class="p-3.5">Status</th>
                                    <th class="p-3.5">Aluno Vinculado</th>
                                    <th class="p-3.5">Certificação</th>
                                    <th class="p-3.5">Responsável</th>
                                    <th class="p-3.5 text-right">Ação</th>
                                </tr>
                            </thead>
                            <tbody id="tabelaModalVagas" class="divide-y divide-slate-100"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- MODAL RELATÓRIO INDIVIDUAL DO PARCEIRO -->
    <div id="modalRelatorio" class="fixed inset-0 bg-black/60 backdrop-blur-sm hidden flex items-center justify-center p-4 z-50">
        <div class="bg-white w-full max-w-4xl rounded-3xl shadow-2xl overflow-hidden max-h-[90vh] flex flex-col p-6 space-y-4">
            <div class="flex justify-between items-center border-b pb-3">
                <h3 class="font-bold text-lg text-purple-900" id="tituloModalRelatorio">📄 Relatório Financeiro e de Bolsas</h3>
                <button onclick="fecharModalRelatorio()" class="font-bold text-lg">✕</button>
            </div>
            <div id="conteudoRelatorio" class="overflow-y-auto space-y-4 text-sm flex-1 p-2"></div>
            <div class="pt-3 border-t flex justify-end gap-2">
                <button onclick="baixarPlanilhaRelatorioParceiro()" class="bg-emerald-700 hover:bg-emerald-800 text-white font-semibold px-4 py-2 rounded-xl text-xs">📥 Baixar Planilha (Excel)</button>
                <button onclick="window.print()" class="bg-purple-900 text-white font-semibold px-4 py-2 rounded-xl text-xs">Imprimir</button>
                <button onclick="fecharModalRelatorio()" class="bg-slate-200 text-slate-700 font-semibold px-4 py-2 rounded-xl text-xs">Fechar</button>
            </div>
        </div>
    </div>

    <!-- MODAL ALUNO -->
    <div id="modalAluno" class="fixed inset-0 bg-black/60 backdrop-blur-sm hidden flex items-center justify-center p-4 z-50">
        <div class="bg-white w-full max-w-md rounded-3xl shadow-2xl p-6 space-y-4">
            <h3 class="font-bold text-lg text-purple-900" id="tituloModalAluno">Vincular Aluno à Bolsa</h3>
            <input type="hidden" id="editIdVaga">
            <input type="hidden" id="editParceiroAtual">
            <div>
                <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Nome do Aluno</label>
                <input type="text" id="nomeAlunoInput" required class="w-full px-4 py-3 border border-slate-200 rounded-2xl uppercase text-sm">
            </div>
            <div>
                <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Data da Solicitação da Bolsa</label>
                <input type="date" id="dataSolicitacaoInput" required class="w-full px-4 py-3 border border-slate-200 rounded-2xl text-sm">
            </div>
            <hr class="border-slate-100 my-2">
            <p class="text-xs font-bold text-purple-900 uppercase">Controle de Certificação</p>
            <div>
                <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Data Solicitação do Certificado</label>
                <input type="date" id="dataCertSolicitadaInput" class="w-full px-4 py-3 border border-slate-200 rounded-2xl text-sm">
            </div>
            <div>
                <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Data Entrega do Certificado</label>
                <input type="date" id="dataCertEntregueInput" class="w-full px-4 py-3 border border-slate-200 rounded-2xl text-sm">
            </div>
            <div class="flex gap-2 pt-2">
                <button onclick="salvarAlunoVinculado()" class="flex-1 bg-purple-900 text-white font-semibold py-3 rounded-2xl">Salvar Aluno</button>
                <button onclick="fecharModalAluno()" class="px-4 bg-slate-200 rounded-2xl">Cancelar</button>
            </div>
        </div>
    </div>

    <script>
        const API_URL = "https://script.google.com/macros/s/AKfycbyMryQQMwcII6kthpcImjWDgIKAI69hqnWbR1m2cZ6Vk5z13PrEuobH-SPPLhYWGFxO7Q/exec";

        let sistema = {
            parceiros: [],
            compras: [],
            vagas: [],
            usuarios: [
                { usuario: 'admin', senha: 'admin123', perfil: 'master', empresa: '' },
                { usuario: 'equipe', senha: 'equipe123', perfil: 'funcionario', empresa: '' },
                { usuario: 'neto', senha: 'neto123', perfil: 'parceiro', empresa: 'NETO' }
            ]
        };

        let sessaoAtiva = null;
        window.parceiroLogadoNome = "";

        function inicializarSistema() {
            document.getElementById('telaLogin').classList.remove('hidden');
            document.getElementById('appPrincipal').classList.add('hidden');
            carregarDadosDaNuvem();
            setInterval(() => {
                if (sessaoAtiva) carregarDadosDaNuvem(false);
            }, 8000);
        }

        async function carregarDadosDaNuvem(mostrarAlerta = false) {
            setSyncStatus("Sincronizando...", "bg-yellow-600");
            try {
                const cacheBuster = "?nocache=" + new Date().getTime();
                let resposta = await fetch(API_URL + cacheBuster);
                let dados = await resposta.json();
                if (dados.parceiros) sistema.parceiros = dados.parceiros;
                if (dados.compras) sistema.compras = dados.compras;
                if (dados.vagas) sistema.vagas = dados.vagas;
                if (dados.usuarios && dados.usuarios.length > 0) {
                    sistema.usuarios = dados.usuarios;
                }

                if (sessaoAtiva) {
                    if (sessaoAtiva.perfil === 'parceiro') {
                        carregarPainelParceiroTelaCheia(window.parceiroLogadoNome);
                    } else {
                        atualizarInterface();
                    }
                }
                setSyncStatus("Sincronizado", "bg-green-600");
                if (mostrarAlerta) alert("Dados sincronizados com sucesso!");
            } catch (e) {
                console.log("Erro ao carregar da nuvem", e);
                setSyncStatus("Erro de Conexão", "bg-red-600");
                if (mostrarAlerta) alert("Erro ao sincronizar com a nuvem.");
            }
        }

        async function enviarDadosParaNuvem(payloadCustom = null) {
            setSyncStatus("Gravando...", "bg-blue-600");
            try {
                let payload = payloadCustom ? payloadCustom : { 
                    parceiros: sistema.parceiros, 
                    compras: sistema.compras, 
                    vagas: sistema.vagas, 
                    usuarios: sistema.usuarios 
                };
                
                let resposta = await fetch(API_URL, {
                    redirect: "follow",
                    method: 'POST',
                    headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                    body: JSON.stringify({ payload })
                });

                if (resposta.ok) {
                    setSyncStatus("Sincronizado", "bg-green-600");
                } else {
                    throw new Error("Falha na resposta do servidor");
                }
            } catch (e) {
                console.log("Erro ao sincronizar:", e);
                setSyncStatus("Erro de Gravação", "bg-red-600");
            }
        }

        function setSyncStatus(text, bgClass) {
            const el = document.getElementById('sync-status');
            if (el) {
                el.textContent = text;
                el.className = `text-xs ${bgClass} text-white px-3.5 py-1.5 rounded-full font-semibold shadow-sm transition-all`;
            }
        }

        function fazerLogin(event) {
            event.preventDefault();
            const usuarioInput = document.getElementById('loginUsuario').value.trim().toLowerCase();
            const senhaInput = document.getElementById('loginSenha').value.trim();

            let userEncontrado = sistema.usuarios.find(u => u.usuario.toLowerCase() === usuarioInput && u.senha === senhaInput);

            if (userEncontrado) {
                sessaoAtiva = { usuario: userEncontrado.usuario, perfil: userEncontrado.perfil, empresa: userEncontrado.empresa || '' };
                document.getElementById('telaLogin').classList.add('hidden');
                document.getElementById('appPrincipal').classList.remove('hidden');
                document.getElementById('labelPerfilLogado').innerText = sessaoAtiva.perfil === 'master' ? 'Admin' : (sessaoAtiva.perfil === 'funcionario' ? 'Funcionário' : 'Parceiro: ' + sessaoAtiva.empresa);

                document.getElementById('btnMenuConfig').classList.toggle('hidden', sessaoAtiva.perfil !== 'master');
                carregarDadosDaNuvem();

                if (sessaoAtiva.perfil === 'parceiro') {
                    window.parceiroLogadoNome = sessaoAtiva.empresa.trim().toUpperCase();
                    document.getElementById('painelVisaoGeral').classList.add('hidden');
                    document.getElementById('painelParceiroTelaCheia').classList.remove('hidden');
                    carregarPainelParceiroTelaCheia(window.parceiroLogadoNome);
                } else {
                    document.getElementById('painelParceiroTelaCheia').classList.add('hidden');
                    document.getElementById('painelVisaoGeral').classList.remove('hidden');
                    voltarPainelPrincipal();
                }
            } else {
                alert("Usuário ou senha incorretos!");
            }
        }

        function fazerLogout() {
            sessaoAtiva = null;
            window.parceiroLogadoNome = "";
            document.getElementById('painelParceiroTelaCheia').classList.add('hidden');
            document.getElementById('painelVisaoGeral').classList.remove('hidden');
            inicializarSistema();
        }

        function atualizarInterface() {
            if (sessaoAtiva && sessaoAtiva.perfil === 'parceiro') return;

            const termo = document.getElementById('inputBuscaParceiro').value.toUpperCase().trim();
            const filtrados = sistema.parceiros.filter(p => p.nome.toUpperCase().includes(termo));

            let html = "";
            if (filtrados.length === 0) {
                html = `<tr><td colspan="6" class="p-8 text-center text-slate-400">Nenhum parceiro encontrado.</td></tr>`;
            } else {
                filtrados.forEach(p => {
                    let pVagas = sistema.vagas.filter(v => v.idParceiro && v.idParceiro.trim().toUpperCase() === p.nome.trim().toUpperCase());
                    let pOcupadas = pVagas.filter(v => v.statusBolsa === "Ocupada").length;
                    let pDisponiveis = pVagas.length - pOcupadas;

                    let btnExcluir = sessaoAtiva.perfil === 'master' ? `<button onclick="excluirParceiro('${p.nome}')" class="px-2.5 py-1 bg-red-50 text-red-600 text-xs font-medium rounded-xl">Excluir</button>` : '';

                    html += `<tr class="hover:bg-slate-50 transition">
                        <td class="p-4 font-bold text-purple-950">${p.nome}</td>
                        <td class="p-4 text-slate-600 text-xs">${p.documento || 'Não informado'}</td>
                        <td class="p-4 text-slate-600 text-xs">${p.contato || 'Não informado'}</td>
                        <td class="p-4 text-center font-bold text-purple-900">${pVagas.length}</td>
                        <td class="p-4 text-center">
                            <span class="px-2 py-0.5 bg-emerald-50 text-emerald-700 text-[11px] font-semibold rounded-lg">🟢 ${pOcupadas} Ocupadas</span>
                            <span class="px-2 py-0.5 bg-amber-50 text-amber-700 text-[11px] font-semibold rounded-lg">🟡 ${pDisponiveis} Disponíveis</span>
                        </td>
                        <td class="p-4 text-right">
                            <button onclick="abrirDetalhesParceiro('${p.nome}')" class="px-3 py-1.5 bg-purple-100 text-purple-900 text-xs font-semibold rounded-xl mr-2">Gerenciar</button>
                            ${btnExcluir}
                        </td>
                    </tr>`;
                });
            }
            document.getElementById('tabelaParceirosLista').innerHTML = html;
        }

        async function salvarNovoParceiro(event) {
            event.preventDefault();
            const nome = document.getElementById('nomeNovoParceiro').value.toUpperCase().trim();
            const documento = document.getElementById('documentoParceiro').value.trim();
            const contato = document.getElementById('contatoParceiro').value.trim();

            if (sistema.parceiros.some(p => p.nome.toUpperCase() === nome)) {
                alert("Este parceiro já está cadastrado!");
                return;
            }

            let novoP = { nome, documento, contato };
            sistema.parceiros.push(novoP);
            fecharModalCadastroParceiro();
            atualizarInterface();
            await enviarDadosParaNuvem();
        }

        async function excluirParceiro(nomeParceiro) {
            if (sessaoAtiva.perfil !== 'master') return alert("Acesso negado.");
            if (confirm(`Deseja realmente excluir o parceiro ${nomeParceiro}?`)) {
                sistema.parceiros = sistema.parceiros.filter(p => p.nome.toUpperCase() !== nomeParceiro.toUpperCase());
                sistema.compras = sistema.compras.filter(c => c.idParceiro.toUpperCase() !== nomeParceiro.toUpperCase());
                sistema.vagas = sistema.vagas.filter(v => v.idParceiro.toUpperCase() !== nomeParceiro.toUpperCase());
                
                atualizarInterface();
                await enviarDadosParaNuvem();
            }
        }

        async function excluirLoteCompra(idCompra, nomeParceiro) {
            if (sessaoAtiva.perfil !== 'master') return alert("Acesso restrito a administradores.");
            if (confirm("Deseja realmente excluir este lote de compra? As bolsas associadas a ele também serão removidas.")) {
                sistema.compras = sistema.compras.filter(c => c.idCompra !== idCompra);
                sistema.vagas = sistema.vagas.filter(v => v.idCompra !== idCompra);
                
                await enviarDadosParaNuvem();
                abrirDetalhesParceiro(nomeParceiro);
                alert("Lote de compra excluído com sucesso!");
            }
        }

        function abrirDetalhesParceiro(nomeParceiro) {
            document.getElementById('modalTituloParceiro').innerText = "Painel do Parceiro: " + nomeParceiro;
            document.getElementById('editParceiroAtualModal').value = nomeParceiro;
            
            let pCompras = sistema.compras.filter(c => c.idParceiro && c.idParceiro.trim().toUpperCase() === nomeParceiro.trim().toUpperCase());
            let htmlHist = "";
            pCompras.forEach(c => {
                let dataF = c.dataCompra ? c.dataCompra.split('-').reverse().join('/') : '-';
                let colunaValor = sessaoAtiva.perfil === 'funcionario' ? '' : `<td class="p-3.5 font-semibold text-purple-900">R$ ${c.valorTotal}</td>`;
                let lancadoPor = c.lancadoPor || 'Sistema';
                let btnAcaoLote = sessaoAtiva.perfil === 'master' ? `<td class="p-3.5 text-right"><button onclick="excluirLoteCompra('${c.idCompra}', '${nomeParceiro}')" class="px-2.5 py-1 bg-red-50 text-red-600 text-xs font-medium rounded-xl">Excluir Lote</button></td>` : '';

                htmlHist += `<tr>
                    <td class="p-3.5">${dataF}</td>
                    <td class="p-3.5 font-medium">${c.qtdBolsas}</td>
                    <td class="p-3.5"><span class="px-2 py-1 bg-purple-100 text-purple-900 rounded-lg text-xs">${c.modalidade || 'EJA'}</span></td>
                    ${colunaValor}
                    <td class="p-3.5"><span class="px-2 py-1 ${c.statusFinanceiro==='PENDENTE'?'bg-amber-100 text-amber-800':'bg-emerald-100 text-emerald-800'} rounded-lg text-xs font-semibold">${c.statusFinanceiro || 'PAGO'}</span></td>
                    <td class="p-3.5 text-slate-600 font-medium">${lancadoPor}</td>
                    ${btnAcaoLote}
                </tr>`;
            });
            document.getElementById('tabelaHistoricoLotesModal').innerHTML = htmlHist;
            if (sessaoAtiva.perfil === 'funcionario') {
                document.getElementById('thValorLoteModal').classList.add('hidden');
            } else {
                document.getElementById('thValorLoteModal').classList.remove('hidden');
            }

            renderizarTabelaVagasGeral(nomeParceiro, 'tabelaModalVagas', false);
            document.getElementById('modalParceiro').classList.remove('hidden');
        }

        function carregarPainelParceiroTelaCheia(nomeParceiro) {
            document.getElementById('tituloPainelParceiroFull').innerText = "Painel do Parceiro: " + nomeParceiro;
            
            let pCompras = sistema.compras.filter(c => c.idParceiro && c.idParceiro.trim().toUpperCase() === nomeParceiro.trim().toUpperCase());
            let htmlHist = "";
            pCompras.forEach(c => {
                let dataF = c.dataCompra ? c.dataCompra.split('-').reverse().join('/') : '-';
                
                htmlHist += `<tr>
                    <td class="p-3.5">${dataF}</td>
                    <td class="p-3.5 font-medium">${c.qtdBolsas}</td>
                    <td class="p-3.5"><span class="px-2 py-1 bg-purple-100 text-purple-900 rounded-lg text-xs">${c.modalidade || 'EJA'}</span></td>
                    <td class="p-3.5 font-semibold text-purple-900">R$ ${c.valorTotal}</td>
                    <td class="p-3.5"><span class="px-2 py-1 ${c.statusFinanceiro==='PENDENTE'?'bg-amber-100 text-amber-800':'bg-emerald-100 text-emerald-800'} rounded-lg text-xs font-semibold">${c.statusFinanceiro || 'PAGO'}</span></td>
                </tr>`;
            });
            document.getElementById('tabelaHistoricoLotesParceiroFull').innerHTML = htmlHist;

            renderizarTabelaVagasGeral(nomeParceiro, 'tabelaVagasParceiroFull', true);
        }

        function renderizarTabelaVagasGeral(nomeParceiro, elementId, isParceiroLogado) {
            let pVagas = sistema.vagas.filter(v => v.idParceiro && v.idParceiro.trim().toUpperCase() === nomeParceiro.trim().toUpperCase());
            let html = "";
            let colspanVazio = isParceiroLogado ? 5 : 7;

            if (pVagas.length === 0) {
                html = `<tr><td colspan="${colspanVazio}" class="p-6 text-center text-slate-400">Nenhuma bolsa encontrada.</td></tr>`;
            } else {
                let contadoresLote = {};
                pVagas.forEach(v => {
                    let idC = v.idCompra || 'lote_geral';
                    if (!contadoresLote[idC]) contadoresLote[idC] = 1;
                    else contadoresLote[idC]++;
                    
                    let compraPai = sistema.compras.find(c => c.idCompra === v.idCompra);
                    let qtdTotalLote = compraPai ? compraPai.qtdBolsas : 1;
                    
                    v.numeroBolsaFormatado = `Bolsa ${contadoresLote[idC]} de ${qtdTotalLote}`;
                });

                pVagas.forEach(v => {
                    let certSolF = v.certSolicitada ? v.certSolicitada.split('-').reverse().join('/') : 'Pendente';
                    let certEntF = v.certEntregue ? v.certEntregue.split('-').reverse().join('/') : 'Não entregue';

                    let infoCert = v.statusBolsa === 'Ocupada' ? `
                        <div class="space-y-0.5 text-xs">
                            <div><span class="text-slate-500">Solicitado:</span> ${certSolF}</div>
                            <div><span class="text-slate-500">Entregue:</span> ${certEntF}</div>
                        </div>` : '-';

                    let responsavelTexto = v.responsavelAcao || '-';

                    if (isParceiroLogado) {
                        html += `<tr>
                            <td class="p-3.5 font-semibold text-purple-900">${v.numeroBolsaFormatado}</td>
                            <td class="p-3.5">${v.modalidade}</td>
                            <td class="p-3.5"><span class="px-2.5 py-1 ${v.statusBolsa==='Disponível'?'bg-amber-100 text-amber-800':'bg-emerald-100 text-emerald-800'} text-xs font-semibold rounded-xl">${v.statusBolsa}</span></td>
                            <td class="p-3.5 font-medium">${v.alunoVinculado || 'Nenhum aluno'}</td>
                            <td class="p-3.5 text-right">${v.statusBolsa === 'Ocupada' ? `<div class="text-xs space-y-0.5"><div>Solicitado: ${certSolF}</div><div>Entregue: ${certEntF}</div></div>` : '-'}</td>
                        </tr>`;
                    } else {
                        let btnAcao = v.statusBolsa === 'Disponível'
                            ? `<td class="p-3.5 text-right"><button onclick="abrirModalAluno('${v.idVaga}', '${nomeParceiro}')" class="px-3 py-1.5 bg-purple-100 text-purple-900 text-xs font-semibold rounded-xl">Vincular Aluno</button></td>`
                            : `<td class="p-3.5 text-right">
                                <div class="flex gap-1 justify-end">
                                    <button onclick="abrirModalAluno('${v.idVaga}', '${nomeParceiro}', '${v.alunoVinculado}', '${v.dataSolicitacao}', '${v.certSolicitada||''}', '${v.certEntregue||''}')" class="px-2.5 py-1 bg-blue-50 text-blue-700 text-xs rounded-xl">Editar</button>
                                    <button onclick="desvincularAluno('${v.idVaga}', '${nomeParceiro}')" class="px-2.5 py-1 bg-red-50 text-red-600 text-xs rounded-xl">Liberar</button>
                                </div>
                            </td>`;

                        html += `<tr>
                            <td class="p-3.5 font-semibold text-purple-900">${v.numeroBolsaFormatado}</td>
                            <td class="p-3.5">${v.modalidade}</td>
                            <td class="p-3.5"><span class="px-2.5 py-1 ${v.statusBolsa==='Disponível'?'bg-amber-100 text-amber-800':'bg-emerald-100 text-emerald-800'} text-xs font-semibold rounded-xl">${v.statusBolsa}</span></td>
                            <td class="p-3.5 font-medium">${v.alunoVinculado || 'Nenhum aluno'}</td>
                            <td class="p-3.5">${infoCert}</td>
                            <td class="p-3.5 text-xs text-slate-600 font-medium">${responsavelTexto}</td>
                            ${btnAcao}
                        </tr>`;
                    }
                });
            }
            document.getElementById(elementId).innerHTML = html;
        }

        function abrirModalAluno(idVaga, parceiro, alunoAtual = '', dataAtual = '', certSol = '', certEnt = '') {
            document.getElementById('editIdVaga').value = idVaga;
            document.getElementById('editParceiroAtual').value = parceiro;
            document.getElementById('nomeAlunoInput').value = alunoAtual;
            document.getElementById('dataSolicitacaoInput').value = dataAtual || new Date().toISOString().split('T')[0];
            document.getElementById('dataCertSolicitadaInput').value = certSol;
            document.getElementById('dataCertEntregueInput').value = certEnt;
            document.getElementById('tituloModalAluno').innerText = alunoAtual ? "Editar Aluno e Certificação" : "Vincular Aluno à Bolsa";
            document.getElementById('modalAluno').classList.remove('hidden');
        }

        async function salvarAlunoVinculado() {
            const idVaga = document.getElementById('editIdVaga').value;
            const nomeAluno = document.getElementById('nomeAlunoInput').value.trim().toUpperCase();
            const dataSolicitacao = document.getElementById('dataSolicitacaoInput').value;
            const certSolicitada = document.getElementById('dataCertSolicitadaInput').value;
            const certEntregue = document.getElementById('dataCertEntregueInput').value;
            const parceiroAtual = document.getElementById('editParceiroAtual').value;
            const autor = (sessaoAtiva && sessaoAtiva.usuario) ? sessaoAtiva.usuario : 'Sistema';

            let vaga = sistema.vagas.find(v => v.idVaga === idVaga);
            if (vaga) {
                vaga.alunoVinculado = nomeAluno;
                vaga.statusBolsa = "Ocupada";
                vaga.dataSolicitacao = dataSolicitacao;
                vaga.certSolicitada = certSolicitada;
                vaga.certEntregue = certEntregue;
                vaga.responsavelAcao = autor;

                fecharModalAluno();
                if (sessaoAtiva && sessaoAtiva.perfil === 'parceiro') {
                    carregarPainelParceiroTelaCheia(window.parceiroLogadoNome);
                } else {
                    renderizarTabelaVagasGeral(parceiroAtual, 'tabelaModalVagas', false);
                }
                await enviarDadosParaNuvem();
            }
        }

        async function desvincularAluno(idVaga, parceiroAtual) {
            const autor = (sessaoAtiva && sessaoAtiva.usuario) ? sessaoAtiva.usuario : 'Sistema';
            let vaga = sistema.vagas.find(v => v.idVaga === idVaga);
            if (vaga) {
                vaga.alunoVinculado = "";
                vaga.statusBolsa = "Disponível";
                vaga.dataSolicitacao = "";
                vaga.certSolicitada = "";
                vaga.certEntregue = "";
                vaga.responsavelAcao = autor;

                if (sessaoAtiva && sessaoAtiva.perfil === 'parceiro') {
                    carregarPainelParceiroTelaCheia(window.parceiroLogadoNome);
                } else {
                    renderizarTabelaVagasGeral(parceiroAtual, 'tabelaModalVagas', false);
                }
                await enviarDadosParaNuvem();
            }
        }

        function toggleCalculoAuto() {
            const marcado = document.getElementById('checkAuto').checked;
            document.getElementById('blocoValorUnitario').classList.toggle('hidden', !marcado);
            if (marcado) atualizarCalculoAutomatico();
        }

        function atualizarCalculoAutomatico() {
            if (!document.getElementById('checkAuto').checked) return;
            const qtd = parseInt(document.getElementById('qtdBolsas').value) || 0;
            const unitario = parseFloat(document.getElementById('valorUnitario').value) || 0;
            let total = qtd * unitario;
            document.getElementById('valorTotal').value = total > 0 ? total.toFixed(2).replace('.', ',') : '';
        }

        async function registrarCompraLocal(event) {
            event.preventDefault();
            const btn = document.getElementById('btnSalvarCompra');
            btn.innerText = "Salvando compra...";
            btn.disabled = true;
            setSyncStatus("Gravando...", "bg-blue-600");

            const idParceiro = document.getElementById('selectParceiroCompra').value;
            const qtdBolsas = parseInt(document.getElementById('qtdBolsas').value);
            const valorTotal = document.getElementById('valorTotal').value;
            const statusFinanceiro = document.getElementById('statusFinanceiro').value;
            const modalidade = document.getElementById('modalidade').value;
            const dataCompra = document.getElementById('dataCompra').value;
            const observacoes = document.getElementById('observacoesCompra').value.trim() || "-";
            const lancadoPor = (sessaoAtiva && sessaoAtiva.usuario) ? sessaoAtiva.usuario : 'Sistema';

            const idCompra = "comp_" + Date.now();

            let novaCompra = { 
                idCompra, idParceiro, qtdBolsas, valorTotal, statusFinanceiro, modalidade, dataCompra, 
                observacoes: observacoes, lancadoPor: lancadoPor
            };

            let novasVagas = [];
            for (let i = 1; i <= qtdBolsas; i++) {
                let v = {
                    idVaga: "vaga_" + Date.now() + "_" + i,
                    idCompra: idCompra,
                    idParceiro: idParceiro,
                    numeroBolsa: `Bolsa ${i}`,
                    modalidade: modalidade,
                    statusBolsa: "Disponível",
                    alunoVinculado: "",
                    dataSolicitacao: "",
                    certSolicitada: "",
                    certEntregue: "",
                    responsavelAcao: ""
                };
                novasVagas.push(v);
            }

            sistema.compras.push(novaCompra);
            novasVagas.forEach(v => sistema.vagas.push(v));

            await enviarDadosParaNuvem();

            document.getElementById('formCompra').reset();
            btn.innerText = "Registrar Compra e Gerar Bolsas";
            btn.disabled = false;
            voltarPainelPrincipal();
            alert("Compra registrada com sucesso!");
        }

        function gerarRelatorioParceiro() {
            const parceiroAtual = sessaoAtiva.perfil === 'parceiro' ? window.parceiroLogadoNome : document.getElementById('editParceiroAtualModal').value;
            gerarRelatorioParceiroPorNome(parceiroAtual);
        }

        function gerarRelatorioParceiroPorNome(nomeParceiro) {
            let dadosParceiro = sistema.parceiros.find(p => p.nome.toUpperCase() === nomeParceiro.toUpperCase()) || { nome: nomeParceiro, documento: '-', contato: '-' };
            let pCompras = sistema.compras.filter(c => c.idParceiro && c.idParceiro.trim().toUpperCase() === nomeParceiro.trim().toUpperCase());
            let pVagas = sistema.vagas.filter(v => v.idParceiro && v.idParceiro.trim().toUpperCase() === nomeParceiro.trim().toUpperCase());
            let ocupadas = pVagas.filter(v => v.statusBolsa === 'Ocupada');

            let totalInvestido = 0;
            let totalPago = 0;
            let totalPendente = 0;
            pCompras.forEach(c => {
                let val = parseFloat(String(c.valorTotal || '0').replace(/\./g, '').replace(',', '.')) || 0;
                totalInvestido += val;
                if ((c.statusFinanceiro || 'PAGO') === 'PENDENTE') {
                    totalPendente += val;
                } else {
                    totalPago += val;
                }
            });

            let taxaOcupacao = pVagas.length > 0 ? Math.round((ocupadas.length / pVagas.length) * 100) : 0;
            let formatMoney = (val) => val.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });

            let html = `
                <div class="space-y-4">
                    <div class="bg-purple-50 p-4 rounded-2xl border">
                        <h4 class="font-bold text-purple-900">${dadosParceiro.nome}</h4>
                        <p class="text-xs text-slate-600 mt-1">CNPJ/CPF: ${dadosParceiro.documento || 'Não informado'} | Contato: ${dadosParceiro.contato || 'Não informado'}</p>
                    </div>

                    <div class="grid grid-cols-2 md:grid-cols-5 gap-3 text-center">
                        <div class="bg-slate-50 p-3 rounded-xl border"><p class="text-[11px] text-slate-500 uppercase font-bold">Investido</p><p class="font-bold text-purple-900 text-sm mt-0.5">${formatMoney(totalInvestido)}</p></div>
                        <div class="bg-slate-50 p-3 rounded-xl border"><p class="text-[11px] text-emerald-700 uppercase font-bold">Pago</p><p class="font-bold text-emerald-800 text-sm mt-0.5">${formatMoney(totalPago)}</p></div>
                        <div class="bg-slate-50 p-3 rounded-xl border"><p class="text-[11px] text-amber-700 uppercase font-bold">Pendente</p><p class="font-bold text-amber-800 text-sm mt-0.5">${formatMoney(totalPendente)}</p></div>
                        <div class="bg-slate-50 p-3 rounded-xl border"><p class="text-[11px] text-slate-500 uppercase font-bold">Bolsas (Ocup./Total)</p><p class="font-bold text-slate-800 text-sm mt-0.5">${ocupadas.length}/${pVagas.length}</p></div>
                        <div class="bg-purple-900 text-white p-3 rounded-xl border shadow-sm"><p class="text-[11px] text-purple-200 uppercase font-bold">Taxa de Ocupação</p><p class="font-bold text-lg mt-0.5">${taxaOcupacao}%</p></div>
                    </div>

                    <div>
                        <h5 class="font-semibold text-slate-700 text-xs uppercase mb-2">Alunos Beneficiados e Certificação</h5>
                        <table class="w-full text-left text-xs border rounded-xl overflow-hidden">
                            <thead class="bg-slate-100">
                                <tr>
                                    <th class="p-2.5">Bolsa</th>
                                    <th class="p-2.5">Modalidade</th>
                                    <th class="p-2.5">Aluno</th>
                                    <th class="p-2.5">Certificado Solicitado</th>
                                    <th class="p-2.5">Certificado Entregue</th>
                                </tr>
                            </thead>
                            <tbody>
                                ${ocupadas.length === 0 ? `<tr><td colspan="5" class="p-4 text-center text-slate-400">Nenhum aluno vinculado.</td></tr>` :
                                    ocupadas.map(o => {
                                        let badgeSol = o.certSolicitada ? `<span class="px-2 py-1 bg-blue-100 text-blue-800 rounded-lg font-semibold">${o.certSolicitada.split('-').reverse().join('/')}</span>` : `<span class="px-2 py-1 bg-slate-100 text-slate-500 rounded-lg">Pendente</span>`;
                                        let badgeEnt = o.certEntregue ? `<span class="px-2 py-1 bg-emerald-100 text-emerald-800 rounded-lg font-semibold">${o.certEntregue.split('-').reverse().join('/')}</span>` : `<span class="px-2 py-1 bg-amber-100 text-amber-800 rounded-lg">Não entregue</span>`;
                                        return `<tr>
                                            <td class="p-2.5 font-medium">${o.numeroBolsaFormatado || o.numeroBolsa}</td>
                                            <td class="p-2.5">${o.modalidade}</td>
                                            <td class="p-2.5 font-bold text-purple-900">${o.alunoVinculado}</td>
                                            <td class="p-2.5">${badgeSol}</td>
                                            <td class="p-2.5">${badgeEnt}</td>
                                        </tr>`;
                                    }).join('')
                                }
                            </tbody>
                        </table>
                    </div>
                </div>
            `;
            document.getElementById('conteudoRelatorio').innerHTML = html;
            document.getElementById('modalRelatorio').classList.remove('hidden');
        }

        function baixarPlanilhaRelatorioParceiro() {
            const parceiroAtual = sessaoAtiva.perfil === 'parceiro' ? window.parceiroLogadoNome : document.getElementById('editParceiroAtualModal').value;
            let dadosParceiro = sistema.parceiros.find(p => p.nome.toUpperCase() === parceiroAtual.toUpperCase()) || { nome: parceiroAtual, documento: '-', contato: '-' };
            let pVagas = sistema.vagas.filter(v => v.idParceiro && v.idParceiro.trim().toUpperCase() === parceiroAtual.trim().toUpperCase());
            let ocupadas = pVagas.filter(v => v.statusBolsa === 'Ocupada');

            let htmlTabela = `
                <html xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:x="urn:schemas-microsoft-com:office:excel" xmlns="http://www.w3.org/TR/REC-html40">
                <head><meta charset="UTF-8"></head>
                <body>
                    <h2>Relatório do Parceiro: ${dadosParceiro.nome}</h2>
                    <p><b>CNPJ/CPF:</b> ${dadosParceiro.documento || 'Não informado'} | <b>Contato:</b> ${dadosParceiro.contato || 'Não informado'}</p>
                    <p><b>Total Contratadas:</b> ${pVagas.length} | <b>Ocupadas:</b> ${ocupadas.length} | <b>Disponíveis:</b> ${pVagas.length - ocupadas.length}</p>
                    <br>
                    <table border="1">
                        <tr style="background-color: #f3e8ff; font-weight: bold;">
                            <th>Bolsa</th>
                            <th>Modalidade</th>
                            <th>Aluno Vinculado</th>
                            <th>Certificado Solicitado</th>
                            <th>Certificado Entregue</th>
                        </tr>
                        ${ocupadas.map(o => `
                            <tr>
                                <td>${o.numeroBolsaFormatado || o.numeroBolsa}</td>
                                <td>${o.modalidade}</td>
                                <td><b>${o.alunoVinculado}</b></td>
                                <td>${o.certSolicitada ? o.certSolicitada.split('-').reverse().join('/') : 'Pendente'}</td>
                                <td>${o.certEntregue ? o.certEntregue.split('-').reverse().join('/') : 'Não entregue'}</td>
                            </tr>
                        `).join('')}
                    </table>
                </body>
                </html>
            `;

            let blob = new Blob([htmlTabela], { type: 'application/vnd.ms-excel;charset=utf-8;' });
            let url = URL.createObjectURL(blob);
            let a = document.createElement('a');
            a.href = url;
            a.download = `Relatorio_${parceiroAtual.replace(/\s+/g, '_')}.xls`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
        }

        function abrirPaginaRelatorioGeral() {
            if (sessaoAtiva.perfil === 'funcionario') {
                return alert("Acesso restrito. Funcionários não visualizam dados financeiros.");
            }

            document.getElementById('secaoGerenciarParceiros').classList.add('hidden');
            document.getElementById('secaoRegistrarCompra').classList.add('hidden');
            document.getElementById('secaoRelatorioGeral').classList.remove('hidden');

            const filtroMod = document.getElementById('filtroModalidadeRelatorio').value;

            let comprasFiltradas = sistema.compras;
            let vagasFiltradas = sistema.vagas;

            if (filtroMod !== 'TODAS') {
                comprasFiltradas = sistema.compras.filter(c => (c.modalidade || 'EJA') === filtroMod);
                vagasFiltradas = sistema.vagas.filter(v => (v.modalidade || 'EJA') === filtroMod);
            }

            let totalInvestido = 0;
            let totalPago = 0;
            let totalPendente = 0;

            comprasFiltradas.forEach(c => {
                let valorNum = parseFloat(String(c.valorTotal || '0').replace(/\./g, '').replace(',', '.')) || 0;
                totalInvestido += valorNum;
                if ((c.statusFinanceiro || 'PAGO') === 'PENDENTE') {
                    totalPendente += valorNum;
                } else {
                    totalPago += valorNum;
                }
            });

            let totalParceiros = sistema.parceiros.length;
            let totalVagas = vagasFiltradas.length;
            let totalOcupadas = vagasFiltradas.filter(v => v.statusBolsa === 'Ocupada').length;
            let totalDisponiveis = totalVagas - totalOcupadas;
            let taxaOcupacao = totalVagas > 0 ? Math.round((totalOcupadas / totalVagas) * 100) : 0;

            let formatMoney = (val) => val.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });

            let html = `
                <div class="space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-6 gap-3 text-center">
                        <div class="bg-purple-50/70 p-4 rounded-2xl border border-purple-100 shadow-sm">
                            <p class="text-[11px] text-slate-500 uppercase font-bold">Investimento Total</p>
                            <p class="font-bold text-purple-900 text-base mt-1">${formatMoney(totalInvestido)}</p>
                        </div>
                        <div class="bg-emerald-50/70 p-4 rounded-2xl border border-emerald-100 shadow-sm">
                            <p class="text-[11px] text-emerald-700 uppercase font-bold">Recebido (Pago)</p>
                            <p class="font-bold text-emerald-800 text-base mt-1">${formatMoney(totalPago)}</p>
                        </div>
                        <div class="bg-amber-50/70 p-4 rounded-2xl border border-amber-100 shadow-sm">
                            <p class="text-[11px] text-amber-700 uppercase font-bold">Pendente</p>
                            <p class="font-bold text-amber-800 text-base mt-1">${formatMoney(totalPendente)}</p>
                        </div>
                        <div class="bg-slate-50 p-4 rounded-2xl border shadow-sm">
                            <p class="text-[11px] text-slate-500 uppercase font-bold">Parceiros</p>
                            <p class="font-bold text-slate-800 text-lg mt-1">${totalParceiros}</p>
                        </div>
                        <div class="bg-slate-50 p-4 rounded-2xl border shadow-sm">
                            <p class="text-[11px] text-slate-500 uppercase font-bold">Bolsas / Ocupação</p>
                            <p class="font-bold text-purple-900 text-lg mt-1">${totalOcupadas}/${totalVagas} <span class="text-xs font-normal text-slate-500">(${taxaOcupacao}%)</span></p>
                        </div>
                        <div class="bg-slate-50 p-4 rounded-2xl border shadow-sm">
                            <p class="text-[11px] text-slate-500 uppercase font-bold">Disponíveis</p>
                            <p class="font-bold text-amber-600 text-lg mt-1">${totalDisponiveis}</p>
                        </div>
                    </div>

                    <div class="bg-white p-6 rounded-3xl border shadow-sm space-y-4">
                        <h3 class="font-bold text-slate-800 text-base">💰 Resumo Financeiro e Lotes por Parceiro</h3>
                        <div class="border rounded-2xl overflow-hidden">
                            <table class="w-full text-left text-sm">
                                <thead class="bg-slate-50 text-xs uppercase text-slate-500 border-b">
                                    <tr>
                                        <th class="p-3.5">Parceiro</th>
                                        <th class="p-3.5 text-center">Lotes Registrados</th>
                                        <th class="p-3.5 text-center">Bolsas Contratadas</th>
                                        <th class="p-3.5 text-right">Valor Total Investido</th>
                                        <th class="p-3.5 text-center">Status Financeiro</th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y divide-slate-100">
                                    ${sistema.parceiros.length === 0 ? `<tr><td colspan="5" class="p-4 text-center text-slate-400">Nenhum parceiro cadastrado.</td></tr>` : ''}
                                    ${sistema.parceiros.map(p => {
                                        let pCompras = comprasFiltradas.filter(c => c.idParceiro && c.idParceiro.trim().toUpperCase() === p.nome.trim().toUpperCase());
                                        let pVagas = vagasFiltradas.filter(v => v.idParceiro && v.idParceiro.trim().toUpperCase() === p.nome.trim().toUpperCase());
                                        if (filtroMod !== 'TODAS' && pCompras.length === 0 && pVagas.length === 0) return '';
                                        
                                        let valorParceiro = 0;
                                        let temPendente = false;
                                        pCompras.forEach(c => {
                                            valorParceiro += parseFloat(String(c.valorTotal || '0').replace(/\./g, '').replace(',', '.')) || 0;
                                            if (c.statusFinanceiro === 'PENDENTE') temPendente = true;
                                        });

                                        let badgeFinanceiro = pCompras.length === 0 ? `<span class="text-slate-400 text-xs">Sem lotes</span>` : 
                                            (temPendente ? `<span class="px-2.5 py-1 bg-amber-100 text-amber-800 text-xs font-semibold rounded-xl">🟡 Pendente</span>` : `<span class="px-2.5 py-1 bg-emerald-100 text-emerald-800 text-xs font-semibold rounded-xl">🟢 Pago</span>`);

                                        return `<tr>
                                            <td class="p-3.5 font-bold text-purple-950">${p.nome}</td>
                                            <td class="p-3.5 text-center font-medium">${pCompras.length}</td>
                                            <td class="p-3.5 text-center font-bold text-purple-900">${pVagas.length}</td>
                                            <td class="p-3.5 text-right font-semibold text-purple-900">${formatMoney(valorParceiro)}</td>
                                            <td class="p-3.5 text-center">${badgeFinanceiro}</td>
                                        </tr>`;
                                    }).join('')}
                                </tbody>
                            </table>
                        </div>
                    </div>

                    <div class="bg-white p-6 rounded-3xl border shadow-sm space-y-4">
                        <h3 class="font-bold text-slate-800 text-base">🎓 Panorama Pedagógico (Alunos e Certificações)</h3>
                        <div class="border rounded-2xl overflow-hidden">
                            <table class="w-full text-left text-xs">
                                <thead class="bg-slate-50 uppercase text-slate-500 border-b">
                                    <tr>
                                        <th class="p-3.5">Parceiro</th>
                                        <th class="p-3.5">Bolsa</th>
                                        <th class="p-3.5">Modalidade</th>
                                        <th class="p-3.5">Aluno Vinculado</th>
                                        <th class="p-3.5 text-center">Certificado Solicitado</th>
                                        <th class="p-3.5 text-center">Certificado Entregue</th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y divide-slate-100 text-slate-700">
                                    ${vagasFiltradas.filter(v => v.statusBolsa === 'Ocupada').length === 0 ? `<tr><td colspan="6" class="p-6 text-center text-slate-400">Nenhum aluno vinculado no filtro selecionado.</td></tr>` : ''}
                                    ${vagasFiltradas.filter(v => v.statusBolsa === 'Ocupada').map(v => {
                                        let badgeSol = v.certSolicitada ? `<span class="px-2.5 py-1 bg-blue-100 text-blue-800 rounded-lg font-semibold">🔵 ${v.certSolicitada.split('-').reverse().join('/')}</span>` : `<span class="px-2.5 py-1 bg-slate-100 text-slate-500 rounded-lg">Pendente</span>`;
                                        let badgeEnt = v.certEntregue ? `<span class="px-2.5 py-1 bg-emerald-100 text-emerald-800 rounded-lg font-semibold">🟢 ${v.certEntregue.split('-').reverse().join('/')}</span>` : `<span class="px-2.5 py-1 bg-amber-100 text-amber-800 rounded-lg font-medium">🔴 Não entregue</span>`;
                                        
                                        return `<tr>
                                            <td class="p-3.5 font-bold text-purple-950">${v.idParceiro}</td>
                                            <td class="p-3.5 font-medium">${v.numeroBolsaFormatado || v.numeroBolsa}</td>
                                            <td class="p-3.5"><span class="px-2 py-0.5 bg-purple-50 text-purple-900 rounded">${v.modalidade}</span></td>
                                            <td class="p-3.5 font-bold text-purple-900 text-sm">${v.alunoVinculado}</td>
                                            <td class="p-3.5 text-center">${badgeSol}</td>
                                            <td class="p-3.5 text-center">${badgeEnt}</td>
                                        </tr>`;
                                    }).join('')}
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            `;
            document.getElementById('conteudoRelatorioGeralPagina').innerHTML = html;
        }

        function baixarPlanilhaRelatorio() {
            const filtroMod = document.getElementById('filtroModalidadeRelatorio').value;
            let vagasFiltradas = filtroMod === 'TODAS' ? sistema.vagas : sistema.vagas.filter(v => (v.modalidade || 'EJA') === filtroMod);
            
            let htmlTabela = `
                <html xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:x="urn:schemas-microsoft-com:office:excel" xmlns="http://www.w3.org/TR/REC-html40">
                <head><meta charset="UTF-8"></head>
                <body>
                    <h2>Relatório Consolidado - Colégio Êxodo (${filtroMod})</h2>
                    <table border="1">
                        <tr style="background-color: #f3e8ff; font-weight: bold;">
                            <th>Parceiro</th><th>Bolsa</th><th>Modalidade</th><th>Aluno Vinculado</th><th>Certificado Solicitado</th><th>Certificado Entregue</th>
                        </tr>
                        ${vagasFiltradas.filter(v => v.statusBolsa === 'Ocupada').map(v => `
                            <tr>
                                <td>${v.idParceiro}</td>
                                <td>${v.numeroBolsaFormatado || v.numeroBolsa}</td>
                                <td>${v.modalidade}</td>
                                <td><b>${v.alunoVinculado}</b></td>
                                <td>${v.certSolicitada ? v.certSolicitada.split('-').reverse().join('/') : 'Pendente'}</td>
                                <td>${v.certEntregue ? v.certEntregue.split('-').reverse().join('/') : 'Não entregue'}</td>
                            </tr>
                        `).join('')}
                    </table>
                </body>
                </html>
            `;

            let blob = new Blob([htmlTabela], { type: 'application/vnd.ms-excel;charset=utf-8;' });
            let url = URL.createObjectURL(blob);
            let a = document.createElement('a');
            a.href = url;
            a.download = `Relatorio_Geral_${filtroMod}.xls`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
        }

        function voltarPainelPrincipal() {
            document.getElementById('secaoRegistrarCompra').classList.add('hidden');
            document.getElementById('secaoRelatorioGeral').classList.add('hidden');
            document.getElementById('secaoGerenciarParceiros').classList.remove('hidden');
            atualizarInterface();
        }

        function abrirPaginaRegistrarCompra() {
            document.getElementById('secaoGerenciarParceiros').classList.add('hidden');
            document.getElementById('secaoRelatorioGeral').classList.add('hidden');
            document.getElementById('secaoRegistrarCompra').classList.remove('hidden');
            document.getElementById('dataCompra').value = new Date().toISOString().split('T')[0];
            document.getElementById('valorTotal').value = '';
            document.getElementById('observacoesCompra').value = '';
            document.getElementById('checkAuto').checked = false;
            document.getElementById('blocoValorUnitario').classList.add('hidden');
            
            let html = '<option value="">-- Escolha um parceiro cadastrado --</option>';
            sistema.parceiros.forEach(p => html += `<option value="${p.nome}">${p.nome}</option>`);
            document.getElementById('selectParceiroCompra').innerHTML = html;
        }

        function verificarPermissaoMaster(acao) {
            if (sessaoAtiva.perfil !== 'master') return alert("Acesso restrito a administradores.");
            acao();
        }

        function abrirModalCadastroParceiro() { document.getElementById('modalCadastrarParceiro').classList.remove('hidden'); }
        function fecharModalCadastroParceiro() { document.getElementById('modalCadastrarParceiro').classList.add('hidden'); }
        function fecharModal() { document.getElementById('modalParceiro').classList.add('hidden'); }
        function fecharModalRelatorio() { document.getElementById('modalRelatorio').classList.add('hidden'); }
        function fecharModalAluno() { document.getElementById('modalAluno').classList.add('hidden'); }
        
        function abrirConfiguracoes() {
            renderizarTabelaUsuarios();
            atualizarSelectEmpresasConfig();
            cancelarEdicaoUsuario();
            document.getElementById('modalConfig').classList.remove('hidden');
        }

        function atualizarSelectEmpresasConfig() {
            let select = document.getElementById('novoUsuarioEmpresaSelect');
            if (!select) return;
            let html = '<option value="">-- Selecione o Parceiro --</option>';
            sistema.parceiros.forEach(p => {
                html += `<option value="${p.nome}">${p.nome}</option>`;
            });
            select.innerHTML = html;
        }

        function toggleSelectEmpresaConfig() {
            const perfil = document.getElementById('novoUsuarioPerfil').value;
            const bloco = document.getElementById('blocoSelectEmpresaConfig');
            bloco.classList.toggle('hidden', perfil !== 'parceiro');
        }

        function renderizarTabelaUsuarios() {
            let html = "";
            sistema.usuarios.forEach((u, index) => {
                let perfilBadge = u.perfil === 'master' ? '<span class="px-2 py-0.5 bg-purple-100 text-purple-900 rounded-lg text-xs font-bold">Admin</span>' : (u.perfil === 'funcionario' ? '<span class="px-2 py-0.5 bg-blue-100 text-blue-800 rounded-lg text-xs font-bold">Funcionário</span>' : '<span class="px-2 py-0.5 bg-amber-100 text-amber-800 rounded-lg text-xs font-bold">Parceiro</span>');
                html += `<tr>
                    <td class="p-3 font-semibold text-slate-800">${u.usuario}</td>
                    <td class="p-3">${perfilBadge}</td>
                    <td class="p-3 text-slate-600">${u.empresa || 'Geral (Escola)'}</td>
                    <td class="p-3 text-right space-x-2">
                        <button onclick="carregarEdicaoUsuario(${index})" class="text-blue-600 text-xs hover:underline font-semibold">Editar</button>
                        <button onclick="excluirUsuario(${index})" class="text-red-600 text-xs hover:underline font-semibold">Excluir</button>
                    </td>
                </tr>`;
            });
            document.getElementById('tabelaUsuariosConfig').innerHTML = html;
        }

        function carregarEdicaoUsuario(index) {
            let u = sistema.usuarios[index];
            document.getElementById('editIndexUsuario').value = index;
            document.getElementById('novoUsuarioLogin').value = u.usuario;
            document.getElementById('novoUsuarioSenha').value = u.senha;
            document.getElementById('novoUsuarioPerfil').value = u.perfil;
            toggleSelectEmpresaConfig();
            atualizarSelectEmpresasConfig();
            if (u.perfil === 'parceiro') {
                document.getElementById('novoUsuarioEmpresaSelect').value = u.empresa;
            }
            document.getElementById('tituloModalConfig').innerText = "⚙️ Editar Acesso de Usuário";
            document.getElementById('btnSalvarUsuarioConfig').innerText = "Salvar Alterações";
            document.getElementById('btnCancelarUsuarioConfig').classList.remove('hidden');
        }

        function cancelarEdicaoUsuario() {
            document.getElementById('editIndexUsuario').value = "-1";
            document.getElementById('novoUsuarioLogin').value = "";
            document.getElementById('novoUsuarioSenha').value = "";
            document.getElementById('novoUsuarioPerfil').value = "funcionario";
            toggleSelectEmpresaConfig();
            atualizarSelectEmpresasConfig();
            document.getElementById('tituloModalConfig').innerText = "⚙️ Gestão de Usuários e Acessos";
            document.getElementById('btnSalvarUsuarioConfig').innerText = "Adicionar";
            document.getElementById('btnCancelarUsuarioConfig').classList.add('hidden');
        }

        async function salvarUsuarioSistema(event) {
            event.preventDefault();
            const editIndex = parseInt(document.getElementById('editIndexUsuario').value);
            const usuario = document.getElementById('novoUsuarioLogin').value.trim();
            const senha = document.getElementById('novoUsuarioSenha').value.trim();
            const perfil = document.getElementById('novoUsuarioPerfil').value;
            const empresa = perfil === 'parceiro' ? document.getElementById('novoUsuarioEmpresaSelect').value : '';

            if (perfil === 'parceiro' && !empresa) {
                alert("Selecione qual empresa o parceiro pertence.");
                return;
            }

            if (editIndex === -1) {
                if (sistema.usuarios.some(u => u.usuario.toLowerCase() === usuario.toLowerCase())) {
                    alert("Este usuário já existe!");
                    return;
                }
                sistema.usuarios.push({ usuario, senha, perfil, empresa });
                alert("Usuário adicionado com sucesso!");
            } else {
                sistema.usuarios[editIndex] = { usuario, senha, perfil, empresa };
                alert("Usuário atualizado com sucesso!");
            }

            cancelarEdicaoUsuario();
            renderizarTabelaUsuarios();
            
            await enviarDadosParaNuvem();
            await carregarDadosDaNuvem();
        }

        async function excluirUsuario(index) {
            if (sistema.usuarios.length <= 1) return alert("Você não pode excluir todos os usuários.");
            if (confirm("Deseja excluir este acesso?")) {
                sistema.usuarios.splice(index, 1);
                renderizarTabelaUsuarios();
                
                await enviarDadosParaNuvem();
                await carregarDadosDaNuvem();
            }
        }
        
        function fecharConfiguracoes() { document.getElementById('modalConfig').classList.add('hidden'); }
    </script>
</body>
</html>
