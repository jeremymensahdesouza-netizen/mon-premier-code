# Import checklist — IA personnelle menzoo (RAG)

Objectif: indexer tes conversations/dossiers pour que l'IA personnelle réponde avec tes propres contenus.

1) Préparer tes exports
   - ChatGPT: exporte les conversations pertinentes (JSON/HTML/TXT). Garde un dossier par année (2023, 2024, 2025).
   - Autres sources (optionnel): CV actuels, docs RQT, Yasmine, Média panafricain, mails importants (PDF/TXT/EML).
   - Supprime/masque toute PII inutile (adresses, numéros) avant import.

2) Arborescence recommandée
   /data_raw/
     /chatgpt/2023/
     /chatgpt/2024/
     /chatgpt/2025/
     /projects/RQT/
     /projects/Yasmine/
     /projects/MediaPanafricain/
     /docs_misc/
   /data_clean/
   /index/

3) Nettoyage & normalisation (rapide)
   - Convertis en UTF‑8.
   - Découpe long textes en blocs ~1 000 tokens.
   - Tagge chaque bloc: {date, source, projet, type: [fait|préférence|décision|tâche], confiance: 0–1}.

4) Indexation (premier jet)
   - Génère des embeddings (ex: bge‑m3).
   - Stocke dans FAISS/Chroma (local) avec métadonnées.
   - Conserve l’ID fichier/lignes pour pouvoir citer la source.

5) Requête type (RAG)
   - « Cherche ‘Yasmine MVP’ dans /chatgpt/2025 et /projects/Yasmine; résume les décisions et liste les dépendances. »
   - « Génère un CV Producteur musical basé sur menzoo_profile.yaml + RAG; 1 page; 5 bullets d’impact. »

6) Confidentialité
   - Héberge en UE; chiffre au repos et en transit.
   - Active un log d’accès local.
   - Prévois un bouton ‘oubli’ (suppression irréversible d’un dossier).

7) Itération
   - Ajoute/retire des sources au besoin.
   - Mets à jour menzoo_profile.yaml à chaque jalon (mensuel).

Astuce: commence avec un sous-ensemble (10–20 conversations clés) puis élargis.
