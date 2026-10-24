<!DOCTYPE html>
<html lang="fr" class="h-full bg-slate-50">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Pointage App</title>
    
    <!-- Balises PWA -->
    <link rel="manifest" href="manifest.json">
    <meta name="theme-color" content="#4f46e5">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <link rel="apple-touch-icon" href="icon.png">

    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body class="h-full font-sans text-slate-900 flex flex-col pb-20 md:pb-0">
    <div class="min-h-full flex flex-col">
        <!-- En-tête -->
        <header class="bg-indigo-600 shadow sticky top-0 z-10">
            <div class="max-w-7xl mx-auto py-4 px-4 flex justify-between items-center">
                <h1 class="text-xl font-bold text-white tracking-tight">⏱️ Pointage</h1>
                <div class="flex gap-2">
                    <button onclick="exportCSV()" class="bg-indigo-700 hover:bg-indigo-800 text-white p-2 rounded-lg text-sm font-medium transition shadow-sm" title="Exporter en CSV">📥</button>
                    <button onclick="resetData()" class="bg-red-600 hover:bg-red-700 text-white p-2 rounded-lg text-sm font-medium transition shadow-sm" title="Réinitialiser">🗑️</button>
                </div>
            </div>
        </header>

        <main class="max-w-7xl mx-auto py-4 px-4 flex-1 w-full space-y-6">
            
            <!-- Statistiques -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-3">
                <div class="bg-white p-4 rounded-xl shadow-sm border border-slate-200">
                    <p class="text-xs font-medium text-slate-500">Solde Cumulé</p>
                    <p id="stat-balance" class="text-xl font-bold mt-1 text-emerald-600">+0h 00m</p>
                </div>
                <div class="bg-white p-4 rounded-xl shadow-sm border border-slate-200">
                    <p class="text-xs font-medium text-slate-500">Heures Sup.</p>
                    <p id="stat-overtime" class="text-xl font-bold text-blue-600 mt-1">0h 00m</p>
                </div>
            </div>

            <!-- Graphique Chart.js -->
            <div class="bg-white p-4 rounded-xl shadow-sm border border-slate-200">
                <h3 class="text-sm font-semibold text-slate-800 mb-2">7 Derniers Jours (Heures)</h3>
                <div class="relative h-40 w-full">
                    <canvas id="weeklyChart"></canvas>
                </div>
            </div>

            <!-- Formulaire -->
            <div class="bg-white p-4 rounded-xl shadow-sm border border-slate-200">
                <h2 class="text-md font-semibold text-slate-800 mb-3">Nouveau Pointage</h2>
                <form id="entry-form" onsubmit="saveEntry(event)" class="grid grid-cols-2 gap-3">
                    <div class="col-span-2 md:col-span-1">
                        <label class="block text-xs font-medium text-slate-700 mb-1">Date</label>
                        <input type="date" id="entry-date" required class="w-full rounded-lg border-slate-300 border px-3 py-2 text-sm">
                    </div>
                    <div class="col-span-2 md:col-span-1">
                        <label class="block text-xs font-medium text-slate-700 mb-1">Catégorie</label>
                        <select id="entry-category" class="w-full rounded-lg border-slate-300 border px-3 py-2 text-sm">
                            <option value="Normal">Travail Normal</option>
                            <option value="Heures Sup">Heures Supplémentaires</option>
                            <option value="Mission">Mission / Déplacement</option>
                            <option value="Récupération">Récupération</option>
                            <option value="Absence Justifiée">Absence Justifiée</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-700 mb-1">Début</label>
                        <input type="time" id="entry-start" value="08:00" required class="w-full rounded-lg border-slate-300 border px-3 py-2 text-sm">
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-700 mb-1">Fin</label>
                        <input type="time" id="entry-end" value="16:00" required class="w-full rounded-lg border-slate-300 border px-3 py-2 text-sm">
                    </div>
                    <div class="col-span-2">
                        <label class="block text-xs font-medium text-slate-700 mb-1">Pause (min) & Notes</label>
                        <div class="flex gap-2">
                            <input type="number" id="entry-break" value="0" min="0" class="w-20 rounded-lg border-slate-300 border px-3 py-2 text-sm" placeholder="Min">
                            <input type="text" id="entry-notes" placeholder="Détails (ex: Chantier...)" class="flex-1 rounded-lg border-slate-300 border px-3 py-2 text-sm">
                        </div>
                    </div>
                    <div class="col-span-2 mt-2">
                        <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-3 rounded-lg font-medium text-sm shadow">Pointer</button>
                    </div>
                </form>
            </div>

            <!-- Historique (Vue Mobile en Cartes) -->
            <div class="mb-4">
                <h3 class="text-md font-semibold text-slate-800 mb-3">Historique</h3>
                <div id="mobile-entries" class="grid grid-cols-1 gap-3">
                    <!-- Cartes injectées ici -->
                </div>
            </div>

        </main>
    </div>

    <script>
        const TARGET_DAILY_HOURS = 7.0;
        let entries = JSON.parse(localStorage.getItem('pointage_entries')) || [];
        let chartInstance = null;

        document.getElementById('entry-date').valueAsDate = new Date();

        // Enregistrement du Service Worker pour la PWA
        if ('serviceWorker' in navigator) {
            navigator.serviceWorker.register('sw.js');
        }

        function saveEntry(e) {
            e.preventDefault();
            const date = document.getElementById('entry-date').value;
            const category = document.getElementById('entry-category').value;
            const start = document.getElementById('entry-start').value;
            const end = document.getElementById('entry-end').value;
            const breakMins = parseFloat(document.getElementById('entry-break').value) || 0;
            const notes = document.getElementById('entry-notes').value;

            const [startH, startM] = start.split(':').map(Number);
            const [endH, endM] = end.split(':').map(Number);
            
            let diffMinutes = (endH * 60 + endM) - (startH * 60 + startM) - breakMins;
            if (diffMinutes < 0) diffMinutes += 24 * 60;
            const hoursWorked = diffMinutes / 60;

            entries.push({ id: Date.now(), date, category, start, end, breakMins, hoursWorked, notes });
            entries.sort((a, b) => new Date(b.date) - new Date(a.date));
            localStorage.setItem('pointage_entries', JSON.stringify(entries));
            
            document.getElementById('entry-notes').value = '';
            renderApp();
        }

        function deleteEntry(id) {
            entries = entries.filter(item => item.id !== id);
            localStorage.setItem('pointage_entries', JSON.stringify(entries));
            renderApp();
        }

        function formatHours(decimalHours) {
            const sign = decimalHours < 0 ? '-' : '+';
            const absHours = Math.abs(decimalHours);
            const h = Math.floor(absHours);
            const m = Math.round((absHours - h) * 60);
            return `${sign}${h}h ${m < 10 ? '0' : ''}${m}m`;
        }

        function renderApp() {
            const container = document.getElementById('mobile-entries');
            container.innerHTML = '';

            let totalBalance = 0;
            let totalOvertime = 0;

            entries.forEach(entry => {
                let diffFromTarget = 0;
                if (['Normal', 'Mission', 'Récupération'].includes(entry.category)) {
                    diffFromTarget = entry.hoursWorked - TARGET_DAILY_HOURS;
                } else if (entry.category === 'Heures Sup') {
                    totalOvertime += entry.hoursWorked;
                    diffFromTarget = entry.hoursWorked;
                }
                totalBalance += diffFromTarget;

                // Carte Mobile
                const card = document.createElement('div');
                card.className = "bg-white p-4 rounded-xl shadow-sm border border-slate-200 relative";
                card.innerHTML = `
                    <div class="flex justify-between items-start mb-2">
                        <div>
                            <p class="text-sm font-bold text-slate-800">${entry.date}</p>
                            <p class="text-xs text-slate-500">${entry.start} à ${entry.end}</p>
                        </div>
                        <span class="px-2 py-1 text-[10px] font-bold rounded-md bg-slate-100">${entry.category}</span>
                    </div>
                    <div class="flex justify-between items-end mt-3">
                        <div>
                            <p class="text-xs text-slate-500">Durée: <span class="font-bold text-slate-700">${entry.hoursWorked.toFixed(1)}h</span></p>
                            <p class="text-xs text-slate-500 truncate max-w-[150px]">${entry.notes || ''}</p>
                        </div>
                        <button onclick="deleteEntry(${entry.id})" class="text-red-500 text-xs font-semibold p-1">Supprimer</button>
                    </div>
                `;
                container.appendChild(card);
            });

            document.getElementById('stat-balance').textContent = formatHours(totalBalance);
            document.getElementById('stat-balance').className = `text-xl font-bold mt-1 ${totalBalance >= 0 ? 'text-emerald-600' : 'text-red-600'}`;
            document.getElementById('stat-overtime').textContent = `${Math.floor(totalOvertime)}h ${Math.round((totalOvertime % 1)*60)}m`;

            updateChart();
        }

        function updateChart() {
            const ctx = document.getElementById('weeklyChart').getContext('2d');
            if (chartInstance) chartInstance.destroy();

            // Prendre les 7 dernières entrées
            const recentEntries = entries.slice(0, 7).reverse();
            const labels = recentEntries.map(e => e.date.substring(5)); // Affiche MM-DD
            const data = recentEntries.map(e => e.hoursWorked);

            chartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Heures',
                        data: data,
                        backgroundColor: '#4f46e5',
                        borderRadius: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: { y: { beginAtZero: true, suggestedMax: 10 } }
                }
            });
        }

        // ... (Les fonctions exportCSV et resetData restent identiques) ...
        renderApp();
    </script>
</body>
</html>
