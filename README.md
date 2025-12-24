# Or-amento-Silwa-Tecnologia
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Orçamento - Silwa Tecnologia</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    
    <style>
        :root {
            /* Cores baseadas na identidade visual da imagem enviada */
            --silwa-purple: #9600c6; /* Roxo vibrante da logo */
            --silwa-dark: #4a0063;
            --silwa-light: #f3e5f5;
            --text-color: #333;
            --border-color: #e0e0e0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
            color: var(--text-color);
        }

        /* Área de Controles (Não sai no PDF) */
        .controls {
            max-width: 900px;
            margin: 0 auto 20px auto;
            text-align: right;
        }

        .btn-pdf {
            background-color: var(--silwa-purple);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            font-weight: bold;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            transition: background 0.3s;
        }

        .btn-pdf:hover {
            background-color: var(--silwa-dark);
        }

        /* Folha A4 simulada */
        .page {
            max-width: 900px;
            margin: 0 auto;
            background: #fff;
            padding: 40px;
            box-shadow: 0 0 20px rgba(0,0,0,0.1);
            border-radius: 8px;
        }

        /* Cabeçalho */
        header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 3px solid var(--silwa-purple);
            padding-bottom: 20px;
            margin-bottom: 30px;
        }

        .logo-container img {
            max-width: 200px; /* Ajuste conforme necessário */
            height: auto;
        }
        
        /* Fallback caso a imagem não carregue */
        .logo-fallback {
            background-color: var(--silwa-purple);
            color: white;
            padding: 15px 25px;
            font-weight: 900;
            font-size: 24px;
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        .company-info {
            text-align: right;
        }

        .company-info h1 {
            margin: 0;
            color: var(--silwa-purple);
            font-size: 1.5rem;
            text-transform: uppercase;
        }

        .company-info p {
            margin: 5px 0 0;
            font-size: 0.9rem;
            color: #666;
        }

        /* Tabela de Serviços */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 30px;
        }

        thead {
            background-color: var(--silwa-purple);
            color: white;
        }

        th, td {
            padding: 12px;
            border-bottom: 1px solid var(--border-color);
            text-align: left;
        }

        th {
            font-weight: 600;
            text-transform: uppercase;
            font-size: 0.85rem;
        }

        /* Inputs dentro da tabela para edição limpa */
        input[type="number"] {
            width: 60px;
            padding: 5px;
            border: 1px solid #ccc;
            border-radius: 4px;
            text-align: center;
            font-size: 1rem;
            color: var(--silwa-purple);
            font-weight: bold;
        }

        /* Seção de Implantação */
        .deployment-section {
            background-color: var(--silwa-light);
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 30px;
            border-left: 5px solid var(--silwa-purple);
        }

        .deployment-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .deployment-header h3 {
            margin: 0;
            color: var(--silwa-dark);
        }

        textarea {
            width: 98%;
            height: 60px;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            resize: vertical;
            font-family: inherit;
            margin-bottom: 10px;
        }

        .deployment-price-row {
            display: flex;
            justify-content: flex-end;
            align-items: center;
            gap: 10px;
        }

        .deployment-price-row input {
            width: 120px;
            text-align: right;
        }

        /* Área de Totais */
        .totals-area {
            text-align: right;
            margin-top: 20px;
        }

        .total-row {
            display: flex;
            justify-content: flex-end;
            align-items: center;
            font-size: 1.1rem;
            margin-bottom: 10px;
            color: #555;
        }

        .grand-total {
            font-size: 2rem;
            color: var(--silwa-purple);
            font-weight: 800;
            margin-top: 15px;
            border-top: 2px solid var(--border-color);
            padding-top: 15px;
            display: inline-block;
        }

        /* Rodapé */
        .footer {
            margin-top: 50px;
            text-align: center;
            font-size: 0.8rem;
            color: #999;
            border-top: 1px solid #eee;
            padding-top: 20px;
        }

        /* Formatação de Moeda */
        .money {
            font-family: 'Courier New', Courier, monospace;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="controls">
        <button class="btn-pdf" onclick="generatePDF()">📥 Baixar Orçamento em PDF</button>
    </div>

    <div class="page" id="element-to-print">
        
        <header>
            <div class="logo-container">
                <img src="IMPLANTAÇÃO.png" alt="SILWA DIGITAL" onerror="this.style.display='none'; document.getElementById('fallback-logo').style.display='block';">
                <div id="fallback-logo" class="logo-fallback" style="display:none;">SILWA DIGITAL</div>
            </div>
            <div class="company-info">
                <h1>Silwa Tecnologia</h1>
                <p>Soluções em Automação e Gestão</p>
                <p>Data: <span id="current-date"></span></p>
            </div>
        </header>

        <table>
            <thead>
                <tr>
                    <th style="width: 50%;">Descrição do Serviço / Módulo</th>
                    <th style="width: 15%; text-align: center;">Qtd.</th>
                    <th style="width: 15%; text-align: right;">Valor Unit.</th>
                    <th style="width: 20%; text-align: right;">Total</th>
                </tr>
            </thead>
            <tbody id="services-body">
                </tbody>
        </table>

        <div class="deployment-section">
            <div class="deployment-header">
                <h3>⚙️ Taxa de Implantação e Configuração</h3>
            </div>
            <textarea id="deploy-desc" placeholder="Descreva aqui os detalhes da implantação (Ex: Treinamento, instalação em 3 terminais, configuração de cardápio digital...)"></textarea>
            
            <div class="deployment-price-row">
                <label><strong>Valor da Implantação:</strong></label>
                <input type="number" id="deploy-price" value="0.00" step="10.00" oninput="updateCalculations()">
            </div>
        </div>

        <div class="totals-area">
            <div class="total-row">
                <span>Total Mensalidade: &nbsp;</span>
                <span id="monthly-total" class="money">R$ 0,00</span>
            </div>
            <div class="total-row">
                <span>Total Implantação (Único): &nbsp;</span>
                <span id="deploy-total-display" class="money">R$ 0,00</span>
            </div>
            <div class="grand-total">
                TOTAL DA PROPOSTA: <span id="grand-total">R$ 0,00</span>
            </div>
        </div>

        <div class="footer">
            <p>Este orçamento tem validade de 10 dias. Valores sujeitos a alteração sem aviso prévio.</p>
            <p>Silwa Tecnologia © 2025</p>
        </div>
    </div>

    <script>
        // Data Atual
        const date = new Date();
        document.getElementById('current-date').innerText = date.toLocaleDateString('pt-BR');

        // Dados dos produtos (Custo + 70% Margem)
        const products = [
            { name: "Gestão", price: 42.62, qty: 1 },
            { name: "Usuário Cloud", price: 0.00, qty: 1 },
            { name: "PDV/Comandas", price: 23.90, qty: 6 },
            { name: "NFCE", price: 40.80, qty: 1 },
            { name: "Estoque", price: 43.86, qty: 1 },
            { name: "Financeiro", price: 42.50, qty: 1 },
            { name: "Validador de Tickets", price: 19.89, qty: 1 },
            { name: "Validador de CPF", price: 19.89, qty: 1 },
            { name: "Conta Assinada", price: 18.26, qty: 1 },
            { name: "PDV Fast", price: 298.25, qty: 1 },
            { name: "Certificado Digital", price: 200.60, qty: 1 },
            { name: "Fidelidade Legal", price: 221.00, qty: 1 },
            { name: "Totem Autoatendimento", price: 168.30, qty: 1 },
            { name: "KDS (Kitchen Display)", price: 85.00, qty: 1 },
            { name: "BI (Business Intelligence)", price: 40.80, qty: 1 },
            { name: "Módulos Gratuitos (iFood, Delivery, etc)", price: 0.00, qty: 1 }
        ];

        const tbody = document.getElementById('services-body');

        function formatCurrency(value) {
            return value.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
        }

        // Renderiza a tabela inicial
        function renderTable() {
            tbody.innerHTML = '';
            products.forEach((product, index) => {
                const tr = document.createElement('tr');
                const priceClass = product.price > 0 ? 'money' : 'money style="color: #bbb;"';
                
                tr.innerHTML = `
                    <td>${product.name}</td>
                    <td style="text-align: center;">
                        <input type="number" id="qty-${index}" value="${product.qty}" min="0" oninput="updateCalculations()">
                    </td>
                    <td ${priceClass} style="text-align: right;">${formatCurrency(product.price)}</td>
                    <td class="money" style="text-align: right;" id="subtotal-${index}">${formatCurrency(product.price * product.qty)}</td>
                `;
                tbody.appendChild(tr);
            });
            updateCalculations();
        }

        // Atualiza os totais
        function updateCalculations() {
            let monthlyTotal = 0;

            // Soma mensalidades
            products.forEach((product, index) => {
                const input = document.getElementById(`qty-${index}`);
                const subtotalEl = document.getElementById(`subtotal-${index}`);
                const qty = parseInt(input.value) || 0;
                const subtotal = qty * product.price;
                
                subtotalEl.innerText = formatCurrency(subtotal);
                monthlyTotal += subtotal;
            });

            // Pega valor da implantação
            const deployInput = document.getElementById('deploy-price');
            const deployValue = parseFloat(deployInput.value) || 0;

            // Atualiza display dos totais
            document.getElementById('monthly-total').innerText = formatCurrency(monthlyTotal);
            document.getElementById('deploy-total-display').innerText = formatCurrency(deployValue);
            
            // Totalzaço (Mensal + Implantação)
            // Nota: Dependendo da regra de negócio, pode-se querer somar a implantação na "Primeira Parcela" ou mostrar separado.
            // Aqui estou somando tudo no "Total da Proposta".
            document.getElementById('grand-total').innerText = formatCurrency(monthlyTotal + deployValue);
        }

        // Função para Gerar PDF
        function generatePDF() {
            const element = document.getElementById('element-to-print');
            
            // Configurações do PDF
            const opt = {
                margin:       [10, 10, 10, 10], // margens top, left, bottom, right
                filename:     'Orcamento_Silwa.pdf',
                image:        { type: 'jpeg', quality: 0.98 },
                html2canvas:  { scale: 2 }, // Melhora a qualidade
                jsPDF:        { unit: 'mm', format: 'a4', orientation: 'portrait' }
            };

            // Executa a conversão
            html2pdf().set(opt).from(element).save();
        }

        renderTable();
    </script>
</body>
</html>
