<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dispatch CORG - Gendarmerie</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #0f172a;
            color: #f8fafc;
            padding: 20px;
        }

        header {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            background: #1e3a8a;
            padding: 20px;
            border-radius: 10px;
            border-bottom: 4px solid #ef4444;
            margin-bottom: 25px;
            gap: 15px;
        }

        .header-title h1 {
            font-size: 1.6rem;
            text-transform: uppercase;
        }

        .header-title p {
            font-size: 0.85rem;
            color: #93c5fd;
            margin-top: 4px;
        }

        .corg-box {
            background-color: #0f172a;
            padding: 12px 18px;
            border-radius: 8px;
            border: 1px solid #3b82f6;
            display: flex;
            flex-direction: column;
            gap: 8px;
            min-width: 300px;
        }

        .corg-box label {
            font-size: 0.85rem;
            font-weight: bold;
            color: #60a5fa;
            text-transform: uppercase;
        }

        .corg-inputs {
            display: flex;
            gap: 10px;
        }

        .actions-bar {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .btn-share {
            background-color: #16a34a;
            color: white;
            border: none;
            padding: 12px 18px;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            font-size: 0.9rem;
        }

        .btn-share:hover {
            background-color: #15803d;
        }

        .btn-clear-all {
            background-color: #dc2626;
            color: white;
            border: none;
            padding: 12px 18px;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            font-size: 0.9rem;
        }

        .btn-clear-all:hover {
            background-color: #b91c1c;
        }

        input, select, textarea {
            background-color: #0f172a;
            border: 1px solid #334155;
            color: #f8fafc;
            padding: 8px 10px;
            border-radius: 6px;
            font-size: 0.9rem;
            width: 100%;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #3b82f6;
        }

        .section-title {
            font-size: 1.2rem;
            margin: 25px 0 15px 0;
            padding-bottom: 8px;
            border-bottom: 2px solid #334155;
            color: #93c5fd;
            text-transform: uppercase;
        }

        .command-title {
            color: #fde047;
            border-bottom-color: #854d0e;
        }

        .command-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .command-card {
            background-color: #1e293b;
            border: 1px solid #334155;
            border-top: 4px solid #eab308;
            border-radius: 10px;
            padding: 16px;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .command-card.section-leader {
            border-top-color: #f97316;
        }

        .command-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .command-header h3 {
            font-size: 1.05rem;
            color: #fef08a;
        }

        .command-badge {
            font-size: 0.72rem;
            padding: 3px 8px;
            border-radius: 4px;
            background-color: #422006;
            color: #fde047;
            font-weight: bold;
        }

        .command-summary {
            font-size: 0.85rem;
            color: #cbd5e1;
            background-color: #0f172a;
            padding: 8px 10px;
            border-radius: 6px;
            border-left: 3px solid #f97316;
        }

        .zones-summary {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .zone-box {
            background-color: #1e293b;
            border: 1px solid #334155;
            border-radius: 8px;
            padding: 15px;
        }

        .zone-box h3 {
            color: #60a5fa;
            margin-bottom: 8px;
            font-size: 1rem;
        }

        .zone-units {
            font-size: 0.9rem;
            font-weight: bold;
            min-height: 24px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 20px;
        }

        .unit-card {
            background-color: #1e293b;
            border: 1px solid #334155;
            border-radius: 10px;
            padding: 16px;
            display: flex;
            flex-direction: column;
            gap: 12px;
            border-top: 6px solid #475569;
        }

        .unit-card.status-dispo { border-top-color: #16a34a; }
        .unit-card.status-patrouille { border-top-color: #2563eb; }
        .unit-card.status-inter { border-top-color: #dc2626; }
        .unit-card.status-indispo { border-top-color: #475569; opacity: 0.85; }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .unit-name {
            font-size: 1.25rem;
            font-weight: bold;
        }

        .unit-type {
            font-size: 0.75rem;
            padding: 3px 8px;
            border-radius: 4px;
            background-color: #334155;
            color: #e2e8f0;
            font-weight: bold;
        }

        .form-group {
            display: flex;
            flex-direction: column;
            gap: 4px;
        }

        .form-group label {
            font-size: 0.8rem;
            color: #94a3b8;
        }

        .leader-label {
            color: #93c5fd !important;
            font-weight: 600;
        }

        .row-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }

        textarea {
            resize: vertical;
            min-height: 55px;
        }

        .btn-reset {
            background-color: #334155;
            color: #cbd5e1;
            border: none;
            padding: 6px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.8rem;
        }

        .btn-reset:hover {
            background-color: #475569;
            color: white;
        }
    </style>
</head>
<body>

<header>
    <div class="header-title">
        <h1>Centre Opérationnel (CORG)</h1>
        <p>Dispatch Gendarmerie - Kavala / Athira / Pyrgos</p>
    </div>

    <div class="corg-box">
        <label>Opérateur(s) CORG en service</label>
        <div class="corg-inputs">
            <input type="text" id="corg_main" placeholder="Opérateur Principal (ex: Maj. Dupont)" oninput="saveAll()">
            <input type="text" id="corg_adj" placeholder="Adjoint CORG" oninput="saveAll()">
        </div>
    </div>

    <div class="actions-bar">
        <button class="btn-share" id="btnShare" onclick="copyShareLink()">Copier le lien à jour</button>
        <button class="btn-clear-all" onclick="resetAll()">Tout vider</button>
    </div>
</header>

<h2 class="section-title command-title">Chaîne de Commandement</h2>
<div class="command-grid">
    <div class="command-card section-leader">
        <div class="command-header">
            <h3>Chef de Section</h3>
            <span class="command-badge">4 Patrouilles / 2 Groupes</span>
        </div>
        <div class="form-group">
            <label>Commandant de Section</label>
            <input type="text" id="cmd_section_name" placeholder="Ex: Lt. Moreau" oninput="saveAll()">
        </div>
        <div class="form-group">
            <label>Supervision (Groupe 01 + Groupe 02)</label>
            <div class="command-summary" id="section_summary">Aucune patrouille affectée</div>
        </div>
    </div>

    <div class="command-card">
        <div class="command-header">
            <h3>Chef de Groupe 01</h3>
            <span class="command-badge">2 Patrouilles</span>
        </div>
        <div class="form-group">
            <label>Gradé Chef de Groupe 01</label>
            <input type="text" id="cmd_g1_name" placeholder="Ex: Adj-Chef Bernard" oninput="saveAll()">
        </div>
        <div class="row-2">
            <div class="form-group">
                <label>Patrouille 1</label>
                <select id="cmd_g1_u1" onchange="saveAll()"></select>
            </div>
            <div class="form-group">
                <label>Patrouille 2</label>
                <select id="cmd_g1_u2" onchange="saveAll()"></select>
            </div>
        </div>
    </div>

    <div class="command-card">
        <div class="command-header">
            <h3>Chef de Groupe 02</h3>
            <span class="command-badge">2 Patrouilles</span>
        </div>
        <div class="form-group">
            <label>Gradé Chef de Groupe 02</label>
            <input type="text" id="cmd_g2_name" placeholder="Ex: MDC Petit" oninput="saveAll()">
        </div>
        <div class="row-2">
            <div class="form-group">
                <label>Patrouille 3</label>
